# Linux
<!-- GFM-TOC -->
* [文件系统](#文件系统)
* [文件操作](#文件操作)
	* [文件与目录基本操作](#文件与目录基本操作)
	* [文件权限](#文件权限)
	* [文档编辑](#文档编辑)
	* [文件描述符](#文件描述符)
* [文本操作](#文本操作)
	* [查看日志](#查看日志)
* [linux 三剑客](#linux-三剑客)
	* [grep](#grep)
	* [awk](#awk)
	* [sed](#sed)
* [进程管理](#进程管理)
	* [查看进程](#查看进程)
	* [后台运行](#后台运行)
	* [孤儿进程和僵尸进程](#孤儿进程和僵尸进程)
* [系统管理](#系统管理)
	* [用户管理](#用户管理)
* [磁盘管理](#磁盘管理)
* [其他](#其他)
<!-- GFM-TOC -->

## 文件系统
在 linux 中，一切皆是文件。操作系统通过文件系统管理文件及数据，磁盘或分区需要创建文件系统之后，才能被操作系统所用，创建文件系统的过程又称之为格式化。ext3、ext4 是 Linux 中主流的文件系统。

创建文件系统
```sh
mke2fs -t ext4 /dev/sda3 #给第一块 SATA 硬盘的 3 号分区创建 ext4 文件系统
mkfs.ext4 /dev/sda3
```

### 目录
/bin 目录是包含一些二进制文件的目录，即可以运行的一些应用程序。
/dev 目录包含设备文件。 其中许多是在启动时或甚至在运行时生成的。
/etc 系统配置文件。 包含系统名称、用户及其密码、网络上计算机名称等
/home 存放用户个人目录
/opt 目录通常编译软件的地方。应用程序最终会出现在 /opt/bin 目录，库会在 /opt/lib 目录中出现。
/usr 包含了应用程序、库、文档、壁纸、图标和许多其他需要应用程序和服务共享的内容

## 文件操作
### 文件与目录基本操作
#### ls
```html
$ ls [-alrtAFR] file|dir
-a 显示所有文件及目录，以'.'开头的不会列出
-l 长模式输出，显示详细信息
-r 相反顺序显示
-t 按照文件修改时间先后排序
```
列出当前目录下所有名称是 s 开头的文件，新的排在后面
```sh
$ ls -ltr s*
```

#### 目录
- mkdir [-mp] dirname 创建目录
- rmdir [-p] dirname 删除目录，只能删除空目录
- pwd 查看当前所在目录，输出绝对路径

-m 配置目录权限；   
-p 递归创建/删除目录。 创建时确保目录名称存在，不存在的就建一个；删除时当子目录被删除后使它也成为空目录的话，则顺便一并删除

#### touch
修改文件时间信息，或新建文件

#### rm
删除文件或目录，使用 rm 删除成功则无法恢复
```html
$ rm [-ir] file|dir
-i 删除前逐一询问
-r 删除目录及里面的文件，目录必须用次参数
```

#### cp
```$ cp [options] sourcedir destdir``` 复制文件或目录
```html
-a 常用于复制目录，保留链接、文件属性，并复制目录下所有文件
-d 复制时保留链接，链接相当于 win 中的快捷方式
-f 覆盖已存在的目标文件且不提示
-i 覆盖已存在的目标文件前，给与提示
-u 仅复制目标目录中不存在的或是文件内容更新的文件
```

#### scp
远程拷贝，支持跨服务器，并提供加密传输。  
使用 ssh 登陆后本机地址不需要给出。也支持不登录直接跨主机拷贝文件，需要提供用户名和密码。
```sh
$ scp [options] [username@source_ip] source_file [username@remote_ip] dir_file
```

#### mv
```mv [-fi] sourcedir destdir``` 移动目标文件

#### file
确定文件类型

#### less
浏览文件内容,可一页一页显示输出

#### ln
为某文件在另外的位置建立一个同步的链接，不会重复占用磁盘空间。linux 文件系统中的 link 可以视为文件的别名。

`ln [options] [源文件或目录] [目标文件或目录]`

- 硬链接： 一个档案可以有多个名称。硬链接以文件副本的形式存在，但不占用实际空间。不允许给目录创建硬链接。硬链接只有在同一个文件系统中才能创建

- 软链接：产生一个特殊的档案，该档案的内容是指向另一个档案的位置。软链接，以路径的形式存在。类似于 Windows 操作系统中的快捷方式。软链接可以跨文件系统 ，硬链接不可以。软链接可以对一个不存在的文件名进行链接。 软链接可以对目录进行链接

给文件创建软链接，如果 A 丢失， A-ln 失效
`ln -s A.txt A-ln` # -s 是软链接的参数

#### cat
显示文件内容并输出
```html
-n 从 1 开始对输出行进行编号
-b 也是编号，但是空白行不编号
```
把 text1 的文档内容加上行号后输入到 text2 中
```sh
$ cat -n text1 > text2
```

#### find
find 可以向其指定丰富的搜索条件（如文件权限、属主、属组、文件类型、日期和大小等）来定位系统中的文件和目录，还支持对搜索到的结果进行多种类型的命令操作。

`find [paths] [expression] [action]`

[paths]： 接收一个或多个路径作为搜索范围，并在该路径下**递归**搜索，空则为当前目录

[expression] : 对结果进行筛选
```
-name '*.txt': 根据文件名称检索，区分大小写
-iname 'xxx': 忽略大小写
-path 或 -ipath： 匹配某个文件或目录的完整路径
-type： 指定文件类型，f 文件，d 目录，l 符号链接
-empty ： 检索空文件或空目录
! -empty: 反义匹配，也可以接其他选项
-user： 检索属于特定用户的文件或目录
-maxdepth n ： 最多递归 n 层，n=1 则只检索当前目录的结果
```

[action] : 将所有检索结果打印至标准输出
```
-delete ： 删除搜索到的文件
-exec： 执行自定义命令
-ls： 流量搜索到的文件或目录的详细信息
```

```sh
find . -name "*.c" # 列出当前目录及子目录下的所有扩展名为 .c 的文件； 用 -iname 忽略大小写
find /usr -path '*/src/*.txt' # 查找 /usr 下所有文件后缀为 txt 的文件，且该文件的父目录必须是 src
find . -type f # 列出当前目录及子目录中的所有一般文件 
find . -ctime -20 # 列出当前目录及子目录下所有最近 20 天更新过的文件
```

#### head 和 tail
```
head filepath 默认显示 file 的前 10 行
head -k filepath 显示 file 的开头 k 行
head -n -k filepath 除最后 k 行外，显示剩余全部内容
```
```
tail filepath 默认显示 file 的后 10 行
tail +20 filepath 显示从 20 行到文件末尾的内容
tail -c 10 filepath 显示 file 的最后 10 个字符
```

#### wget
wget [options] url 用于从网络上下载资源

-b 启动后转入后台执行，可以用 tail -f wget-log 查看下载进度
-c 断点续传
-o <filename> 保存下载信息(wget-log)到 file 中

下载文件并以新文件名保存
```sh
wget -O new_filename url
```

#### tar
```
-c 建立新的压缩文件
-x 从压缩文件中提取文件
-v 显示操作过程
-f 指定压缩文件
-z 支持 gzip 解压
-j 支持 bzip2 解压
```

打包
```
tar -cvf filename.tar dirName
tar -zcvf filename.tar.gz dirName
tar -jcvf filename.tar.bz2 dirName
```
解压 xvf, zxvf, jxvf
```tar -xvf filename.tar```

### 文件权限
```
rwx； x：可执行
十个字符；第一个表文件类型，- 普通文件，d 目录；c 字符设备文件， b块设备文件；l 符号链接，权限是虚拟的，真是权限为指向的文件，一直是lrwxrwxrwx
后面分别为owner，group， world的权限
```

#### 1.chmod
```chmod [options] mode file``` 修改文件或目录权限

mode: 权限设置字串，格式为 [ugoa][+-=][rwxX][...]
```
u：文件所有者； g：用户组； o：其他所有人； a：all
+：增加权限； -：取消权限； =：设定唯一权限
```

将文件 file1 与 file2 设为该文件拥有者，与其所属同一个群体者可写入，但其他以外的人则不可写入 
```sh
$ chmod ug+w,o-w file1 file2
```

#### 2. chown
```chown [options] user[:group] file``` 修改文件的属主，可改为其他用户或群组

将文件 file 的所有者设为  users 群组中的 tom 用户
```sh
$ chown tom:users file
```

#### 3. chgrp
```chgrp [options] [所属群组] [file/dir]``` 修改文件或目录的所属群组
 
### 文档编辑
#### wc
```wc [-wlc] filename``` 无参数的话默认输出计算文件的字数、行数、字节数  

-w 只显示字数； -l 只显示行数； -c 只显示 byte 数

#### tr
`tr [options] [第一字符集] [第二字符集]` 用于转换或删除文件中的字符

```
-c 反选设定字符，即符合 SET1 的部分不做处理，不符合的才转换
-d 删除指定字符
```

字符集有：  
[:alnum:] 所有字母与数字； [:alpha:] 所有字母； [:digit:] 所有数字  
[:blank:] 所有水平空格； [:space:] 所有水平与垂直空格符； [:punct:] 所有标点符号  
[:graph:] 所有可打印字符（不包含空格）； [:print:] 所有可打印字符(包含空格)  
[:upper:] 所有大写字母； [:lower:] 所有小写字母

将 file 中的所有小写字母转为大写字母
```sh
cat filename | tr [:lower:] [:upper:]
```

### 文件描述符
0: 标准输入 STDIN
1： 标准输出 STDOUT
2： 标准错误输出 STDERR

```sh
cat /proc/sys/fs/file-max # 系统最大打开的文件描述符数
ulimit -n # 进程最多打开文件描述符数
```

## 文本操作
### 查看日志
1. tail
```sh
tail -10f test.log # 实时监控 10 行日志
tail -n 10 test.log # 查询日志尾部最后 10 行日志
tail -n +10 test.log # 查询 10 行之后的所有日志
```

2. head
```sh
head -n 10 test.log # 查询日志头 10 行
head -n -10 test.log # 查询除了最后 10 行外的所有日志
```

3. cat
也可以用 tac，是 cat 的倒序查看
```sh
cat -n test.log | grep "debug" # 查询关键字的日志，并得到行号
```

## linux 三剑客
### grep
grep : 作用 文本搜索工具，根据用户指定的‘模式’（可以是正则表达式）对目标文件逐步进行匹配检查，打印匹配到的行

grep [options] 字符串 [filepath]

-c 显示符合要求的个数； 
-i 忽略大小写；
-n 输出行号；
-v 反向输出，也就是不匹配的内容； 
-o 只显示被匹配到的字符串；
-f <规则文件> 查找符合指定规则文件的内容，格式为每行一个规则样式；

若希望输出匹配行的前后行： 
- grep 字符串 filepath -A 1 ： 输出除匹配的该行外，还显示其后面一行(After 1)
- grep 字符串 filepath -B 1 ： 输出除匹配的该行外，还显示其前面一行(Before 1)
- grep 字符串 filepath -1 ： 输出除匹配的该行外，还显示前一行和后一行

### awk
用于处理数据和生成报告，更适合文本格式化，对文本进行较复杂的格式处理。

```awk [options] 'pattern{action}' filepath``` ，必须用单引号

-F 指定分隔符，如果有多个分隔符： ```awk -F '[:,]' filepath```

awk 逐行处理文本，处理的最小单位是字段，每个字段的命名方式为：$n，n 为字段号，从 1 开始，$0 表示一整行。

**内建变量：**
```  
$0 整行, $1-$n 第n个字段
NR 已经读出的记录数，即行号，从 1 开始，有多个文件的话值也是不断累加的，用于最后可以输出总共的记录数。
FNR 当前记录数，是每个文件自己的行号
OFS 输出字段分隔符，默认为空格
ORS 输出记录分隔符，默认为换行符
```

**awk 编程结构：**  
```sh
awk 'BEGIN{BEGIN 操作} {文件行处理块} END{END 操作}' filepath
```
pattern 包含两种特殊模式:  
- BEGIN 模块是在文件输入前执行的，不输入任何文件数据也会执行该模块，常用于设置修改内置变量如 OFS,RS 等，为用户自定义的变量赋初始值或者打印标题信息等。 操作语句以 ";" 或分行隔开。 可缺省。  
- END 模块是处理完文件后的操作

**重定向：**    
符号与 shell 相同； 目标文件必须用双引号括起；目标文件打开就一直保持打开状态，显式关闭或 awk 程序终止。

awk 每次只能打开打开一个管道，管道右边的命令必须用双引号括起。


查看最近 5 条登录用户和 ip 地址
```sh
$ last -n 5 | awk '{print $1"\t"$3}'
```

过滤文本，查看 /etc/passwd 文件
```sh
$ awk -F ":" '{print NR, $1, $5, $6}' OFS="\t" /etc/passwd
```

字符串匹配，~ 表示模式开始，/pattern/ 中间是模式， ```|| NR==1``` 打印出第一行（有时候是想打印表头），用 !~ // 表示模式取反
```sh
awk -F ":" '$1 ~/er/ || NR==1 {print NR, $1, $5, $6}' OFS="\t" /etc/passwd
```

拆分文件，使用重定向，输出
```sh
awk -F ":" '{if($1 ~/yi/) print > "1.txt"; else print > "2.txt"}' passwd
```

统计，统计每个用户的进程占了多少内存（计算 RSS 列）
```sh
ps aux | awk 'NR!=1{a[$1]+=$6;} END {for (i in a) print i "," a[i]"KB";}'
```

python 编程
```python
instance_id = os.popen('grep \"Log view:\" %s -A 1| awk -F "&" \'{print $3}\' | awk -F "=" \'{print $2}\' | awk \'{if($0!="") print}\'' % job_trace_log_file).readlines()
```

### sed
stream editor , 流编辑器，是一个文本编辑工具，实现数据的替换，删除，增加，选取等(以行为单位进行处理)

```sed [-nri][-e<script>][-f<script文件>] '动作' filepath```

-f<script文件> 将 sed 动作写在文件内，以指定的 script 来处理输入的文本
-i 直接修改读取的文件内容，不输出到终端，也可选择将修改重定向到一个新的文件

动作说明：
a 新增，a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)
i 插入，在当前行之前插入文本。多行时除最后一行外，每行末尾需用"\"续行
d 删除行
s 替换，搭配正则表达式，如 's/old/new/g'

在每行最前面或最后面添加 #
```sh
sed 's/^/#/g' filepath
sed 's/$/#/g' filepath
```

指定需要替换的内容，允许多个匹配，用分号隔开
```sh
sed '3s/old/new/g' filepath # 替换第 3 行的
sed '3,6s/old/new/g' filepath # 替换第 3-6 行的
sed 's/old/new/1' filepath # 替换每行的第一个
sed 's/old/new/3g; xxx' filepath # 替换每行的第三个以后的
```

使用 & 表示被匹配的变量，在周围添加内容
```sh
sed 's/my/[&]/g' filepath # 将所有的 my 变为 [my]
```

## 进程管理
### 查看进程
#### 1. ps
```
空 显示自己的进程；
-a 显示现行终端下的所有进程，包括其他用户的进程；
-A 所有进程都显示，相当于 -e；
-u 以用户为主的进程状态；
x 通常与 -a 一起用，列出较完整的信息；
-l 显示较详细的信息
```

查看系统所有进程
```sh
$ ps aux
```
查看特定进程
```sh
$ ps aux | grep xxx
```

#### 2. pstree
显示进程树，即用树状图形式显示进程。 -p 显示 pid

#### 3. top
可以查看系统的 cpu、内存、运行时间、交换分区、执行的线程等。能够有效发现系统的缺陷在哪。
可以实时显示进程信息，可用于监控 linux 的系统状况

- 第一行 load average 后面有三个数字，显示距离现在 1、5、15 分钟的负载情况，数值除以逻辑 cpu 的数量，结果高于 5 则表明系统在超负荷运转。  
- 第三行 ```%Cpu(s): 13.7 us,  1.5 sy,  0.0 ni, 84.2 id,  0.6 wa,  0.0 hi,  0.0 si,  0.0 st```
```
us: user 用户空间占用 cpu 的百分比 
sy: system 内核空间占用 cpu 的百分比 
ni: niced 改变过优先级的进程占用 cpu 的百分比 
id: 空闲 cpu 百分比 
wa: IO wait IO 等待占用 cpu 的百分比 
hi: Hardware IRQ 硬中断占用 cpu 的百分比 
si: software 软中断占用 cpu 的百分比 
st: 被 hypervisor 偷去的时间
```
- 第四行为内存状态
- 第五行为 swap 交换分区
- 第七行是各进程的监控
```
PR： 进程优先级 
NI： nice 值。负值表示高优先级，正值表示低优先级 
VIRT： 进程使用的虚拟内存总量，VIRT = SWAP + RES 
RES： 进程使用的、未被换出的物理内存大小，RES = CODE + DATA 
SHR： 共享内存大小
S： 进程状态。 D = 不可中断的睡眠状态，R = 运行，S = 睡眠，T = 跟踪/停止，Z = 僵尸进程 
%CPU： 上次更新到现在的CPU时间占用百分比
%MEM： 进程使用的物理内存百分比 
TIME+： 进程使用的CPU时间总计
COMMAND： 进程名称（命令名/命令行）
```

#### 4. netstat
显示各种网络相关信息，如网络连接、路由表、接口状态等。
```
-a 显示所有选项（包括 listen）；
-t 仅显示 tcp 相关； 
-u 仅显示 udp 相关；
-l 仅列出有在 listen 的服务状态；
-n 拒绝显示别名（显示数字）；
-p 显示建立相关连接的程序名
```

查看占用 80 端口的进程信息
```sh
$ netstat -anp | grep 80
```

### 后台运行
```
&：命令后加&，后台运行
bg %1 ： 将1号进程移到后台
fg %1：移到前台
```

### 孤儿进程和僵尸进程
子进程和父进程的运行是异步过程，即父进程永远无法预测子进程何时结束。当子进程完成工作终止后，父进程需要调用 wait() 或 waitpid() 系统取得子进程的终止状态。

#### 孤儿进程
- 一个父进程退出，而他的子进程还在运行，那么这些子进程将成为孤儿进程。
- 孤儿进程没有父进程，会被 init 进行（pid=1）收养，并由 init 进程对他们完成状态收集工作。 
- 孤儿进程不会对系统造成危害。

#### 僵尸进程
- 一个进程使用 fork 创建子进程，如果子进程退出，而父进程没有调用 wait() 或 waitpid() 获取子进程的状态信息，那子进程的进程描述符仍保留在系统中，成为僵尸进程。
- 子进程在 exit() 后并非马上消失，而是留下一个僵尸进程(zombie)的数据结构，等待父进程处理。若父进程没来得及处理，用 ps 查看子进程会显示状态 “Z”
- 系统能使用的进程号有限，如果产生大量僵尸进程，就可能因为没有可用进程号而不能产生新进程。
- 消灭僵尸进程： kill 父进程，那僵尸进程将变为孤儿进程，由 init 收养，init 会释放僵尸进程占用的资源。

### 系统管理
#### 用户管理
```
useradd xxx：添加用户
passwd xxx： 为新用户设置密码
userdel xxx：删除用户
logout：注销当前用户
```

### 磁盘管理
Linux磁盘管理常用三个命令为 df、du 和 fdisk。
```
df：列出文件系统的整体磁盘使用量
du：检查磁盘空间使用量
fdisk：用于磁盘分区
```

#### 1. df
检查文件系统的磁盘空间占用情况，可以获取硬盘被占用了多少空间，目前还剩多少空间等信息。
```sh 
$ df [-ahikHTm] [目录或文件名]
-a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统；
-h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示；
-T ：显示文件系统类型, 连同该 partition 的 filesystem 名称 (例如 ext3) 也列出；
```

#### 2. du
du 命令是对文件和目录磁盘使用的空间的查看
```sh
$ du [-ahskm] 文件或目录名称
```

#### 3. fdisk
fdisk [-l] 装置名称  是磁盘分区表操作工具
-l ：输出后面接的装置所有的分区内容。若仅有 fdisk -l 时， 则系统将会把整个系统内能够搜寻到的装置的分区均列出来。

#### 4. mount
磁盘挂载使用 mount 命令，卸载使用 umount 命令。
mount [-t 文件系统] [-L Label名] [-o 额外选项] [-n]  装置文件名  挂载点
```sh
# 将 /dev/hdc6 挂载到 /mnt/hdc6 上面
$ mount /dev/hdc6 /mnt/hdc6
```






### 过滤器
sort： 可以改变输出结果，生成一个有序列表
uniq： 报道或忽略重复行，接受数据有序列表，常与sort连用; 输出重复的行，加上 -d
如 ls /bin /usr/bin | sort | uniq | less
wc： 显示文件包含的行数、字数和字节数； wc -l ：只显示行数
head/tail ： 默认打印文件开头/结尾的十行； -n x：控制打印x行； -f：检测文件变化，有新内容会显示在屏幕上



wget 地址：下载文件
tar -zxvf xxx：解压； ./configure ； make ； make install
tough filename：新建文件；vi filename：新建并编辑

linux字符类 [:alnum:] 任意一个字母或数字; [:alpha:]; [:digit:]; [:lower:]; [:upper:]
例： \*[[:lower:]123] 文件名以小写字母结尾，或以1 2 3结尾的文件
两次tab键 ： 显示自动补全列表
history：显示历史命令； history | grep /usr/bin ： 显示包含/usr/bin的历史命令

~ ： 显示目录

ctrl+a ： 光标移到行首； ctrl+e ： 光标移到行尾
文本编辑
ctrl+d ： 删除光标位置的字符

### 其他
#### 1. rsync
数据镜像备份工具，用于文件同步和数据传输，可将客户机和远程文件服务器之间的文件同步。
rsync -zr --progress 10.77.29.68::backup/weiflow/xxx
-z 传输时对数据压缩
-r 对子目录递归
--progress 显示数据镜像同步过程

#### 2. curl
curl [options] url ，利用 url 规则在命令行下工作的文件传输工具，支持文件的上传和下载

```sh
curl url ，显示 url 的 html，可重定向保存
curl -c cookie.txt url ，保存 http 的 response 里的 cookie 信息
curl -c cookie.txt -F name=xieyiyu -F pwd=xxx url ，模拟表单信息，模拟登录 url，并保存 cookie 信息
```

#### 3.tr


#### 4. source
source：使当前shell读入路径为filepath的shell文件并依次执行文件中的所有语句，通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录

~/是进入当前用户的主目录。比如我用的用户名是USER 那么命令 cd ~/ 就进入了/home/USER 目录。

.bashrc 是进入.bashrc文件夹，就是用户目录下的名字是.bashrc的目录。

更新配置文件命令： `source ~/.bashrc`

#### 5. xargs
xargs 是给命令传递参数的一个过滤器，也是组合多个命令的一个工具不，一般和管道一起使用。 有些命令不支持管道 | 来传递参数，就需要用 xargs

`find /usr -name '.txt' | xargs ls -l` 如果不加 xargs 会 ls -l 当前目录下所有文件的信息 

递归删除指定文件名的文件
```sh
find . -name '.txt' | xargs rm -f
find . -name '.txt' -delete
```