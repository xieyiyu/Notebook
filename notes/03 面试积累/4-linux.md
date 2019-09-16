### 进程
1. 查看进程 `ps aux | grep xxx`, `pstree`, `top`

2. 找到共用80端口的进程 
```sh
netstat -anp | grep 80
```

3. 查看某个进程的端口号：
```sh
netstat -anp | grep xxx 
lsof -i :80
``` 

4. top： 用于实施监控 linux 系统状况，可以查看 cpu、内存、进程、运行时间等

5. Kill -9 和 kill的区别
kill 用法： kill -n pid,  -n 是信号编号

kill pid 就是 kill -15 pid， -15 是 SIGTERM
系统会发送一个 SIGTERM 的信号给对应的程序。当程序接收到该 signal 后，将会发生以下的事情
- 程序立刻停止
- 当程序释放相应资源后再停止
- 程序可能仍然继续运行

大部分程序接收到 SIGTERM 信号后，会先释放自己的资源，然后在停止。但是也有程序可以在接受到信号量后，做一些其他的事情，并且这些事情是可以配置的。如果程序正在等待IO，可能就不会立马做出相应。也就是说，SIGTERM 多半是会被阻塞的、忽略。

kill -9 pid, -9 s 是 SIGKILL，Kill(can't be caught or ignored) (POSIX)，不管怎样都 kill

6. 杀死占用指定端口的进程
```sh
netstat -anp | grep 端口号 # 先找到 pid
kill -9 pid # 再杀死
```

7. linux 暂停一个进程或程序
暂停： 在 shell窗口 ctrl + z，显示 `[3]+  Stopped ...`
恢复： fg %3

8. 
netstat： 显示网络状态
ping： 测两台主机之间的连通性
ifconnfig：功能是显示或设置网络设备

### vim
1. 显示行号： 命令模式下输入 `:set nu`, 
   取消显示行号： `:set nonu`

2. 替换字符串： 
```sh
:s/old/new/g # 用 old 替换 new，替换当前行的所有匹配
:%s/old/new/g # 用 old 替换 new，替换整个文件的所有匹配
```
用 sed 是： sed 's/old/new/g' file

### 文件操作
#### 文件权限
1. 权限修改 `chmod [ugoa] [+-=][rwx] filepath`

2. 属主修改 `chown [options] username[:groupname] filepath`

3. 群组修改 `chgrp [options] groupname filepath`

#### 增删查改
1. 查找当前目录下名字带有 abc 的文件 `ls *abc*`

2. 创建新文件 `touch newfile`

使用 shell 新建以 00-99 为文件名的空文件
如果是 0-99，可以 touch {0..99}，同样的 mkdir，rm 都可以这样用，同样也可以 touch {0,1,2,3}

如果是 00-99，就需要格式化，一位数的话前面要补 0
```sh
for i in $(seq 0 99); 
do
	filename=$(printf %02d $i); 
	touch "$filename"; 
done
```

3. 服务器A上的文件拷贝到B，远程拷贝 `scp A/xxx B/xxx`

4. 递归删除指定后缀名的文件,如 .txt 
```sh
find . -name '.txt' | xargs rm -f
find . -name '.txt' -delete
```

5. 文件压缩与解压
```sh
压缩： tar -cvf xxx.zip dirname
解压： tar -xvf xxx.zip
```

6. 创建软连接
```sh
ln -s A.txt A-link
```

### 目录操作
1. 查看目录大小
```sh
du -sh # 显示当前目录大小
du -sh dirname/filename # 显示当前目录下的指定目录或文件的大小
ls -l # 也可以查看目录或文件大小
```

2. 递归列出一个目录下所有目录和文件
```sh
find $PWD | xargs ls -d # $PWD 当前路径，-d 是列出绝对路径
find . | xargs ls -d 
```

3. 查看文件或目录的个数
```sh
ls -l | grep "^-" | wc -l # 查看当前目录下的文件个数，文件用 ls -l 开头是 -
ls -l | grep "^d" | wc -l # 查看当前目录下的目录个数
ls -l -R | grep "^-" | wc -l # 查看当前目录及其子目录下的文件个数（-R 递归）
find . -type f | wc -l # 查看当前目录及其子目录下的文件个数
find . -type d | wc -l # 查看当前目录及其子目录下的目录个数（注意会包含 . 这个当前目录）
```

### 文本操作
1. 一个文件夹内批量替换文本
```sh
sed -i "s/old_string/new_string/g" `grep -rl "old_string" /path`
```
grep -r : 递归查询子目录； -l：查询多文件的时候只输出包含匹配字符的文件名
因此 grep -rl： 查找子目录，匹配后只输出文件名

\`\` :反引号，获取执行命令的结果 

2. 用 sed 命令删除文件的 xxx
```sh
sed -i '$d' test.txt # 删除最后一行
sed -i '1d' test.txt # 删除第一行
sed -i '/^$/d' test.txt # 删除所有空行
sed -i 'Nd' test.txt # 删除第 N 行，N 是数字
sed -i '3,5d' test.txt # 删除第 3-5 行
sed -i '/abc/d;/egf/d' test.txt # 删除包含字符串 abc 或 egf 的行
```

3. 查找文本中 “abcd” 字符串出现的次数
使用 vim 统计，在命令模式下输入： `:%s/abcd//gn`，注意如果是 `:%s/abcd/gn` 是用 gn 去替换 abcd
使用 grep 统计 ： `grep -o "abcd" filepath | wc -l`

4. 统计日志文件中一秒之内打印出的日志条数


5. 统计文本中每个单词出现的次数
```sh
cat word.txt | awk '{a[$0]++} END{for (i in a) print i"="a[i]}' # 每行是一个单词
```
如果每行是一个单词，那么直接可以：
```sh
cat word.txt | sort | uniq -c
```

6. 统计出现频率最多的 3 个单词
```sh
cat word.txt | awk '{a[$0]++} END{for (i in a) print i" "a[i]}' | sort -k2rn | head -3 
# -r 倒序； -k2 按照第 2 个字段排序，也就是 a[i]； -n 按照数值排序
```

7. 统计一个文件中出现次数最多的 ip， 文本第二个字段是 ip
```sh
cat ip.txt | awk '{print $2}' | sort | uniq -c | sort -nr | head -n 1
# uniq 命令用于检查及删除文本文件中重复出现的行列，一般与 sort 命令结合使用, -c或--count 在每列旁边显示该行重复出现的次数。
```

### 其他
1. 查看两台服务器是否连通
如果只是测网络是否通： ping ip
如果查看本机与服务器的端口是否连通： curl [IP地址]:[端口号]

2. Linux下可以有多少个文件描述符
```sh
cat /proc/sys/fs/file-max # 系统最大打开的文件描述符数
ulimit -n # 进程最多打开文件描述符数
```

3. 如何调试一个 core 文件
core 文件： 在程序不寻常退出时，内核会在当前工作目录下生成一个 core 文件（是一个内存映像，同时加上调试信息，保留了 Crash 的现场）。使用 gdb 来查看 core 文件，可以指示出导致程序出错的代码所在文件和行数。

通过 gdb 进行调试

4. gdb 的使用

5. 在 Linux 上生成一个可执行文件的过程
Linux下 gcc 编译 c 文件为可执行文件分为四个步骤： 分别是 预编译、编译、汇编、链接

#### 预编译( 生成 hello.i 文件)
预编译器 cpp 把源代码文件和相关的头文件（如stdio.h）预编译成一个 .i 文件
```sh
$ gcc -E hello.c -o hello.i 或者 $ gcc  hello.c > hello.i
```

#### 汇编(生成 hello.o文件)
汇编是 汇编器as 把汇编代码转变成中间目标文件。
```sh
$ gcc -S hello.i -o hello.s 或者 $ gcc -S hello.c -o hello.s
```

#### 编译(生成汇编代码 hello.s)
编译过程是编译器 gcc 把预处理完的文件进行词法分析、语法分析、语义分析及优化后生成相应的汇编代码文件。
```sh
$ gcc -c hello.s -o hello.o 或者 $ gcc -S hello.c -o hello.o
```

#### 链接（生成可执行程序）
链接器 ld：负责将程序的目标文件与所需的所有附加的目标文件连接起来，附加的目标文件包括静态连接库和动态连接库
```sh
$ gcc hello.o -o hello
$ ./hello # 运行
```

6. linux 中的 wget、curl、scp
linux 服务器从互联网中下载文件有三种方式
```sh
wget http://www.xxx.com/1.txt
curl -o 1.txt http://www.xxx.com
scp 远程服务器用户名@远程服务器ip: 远程文件的路径 本地路径
```

7. 后台运行
```sh
nohup python test.py >> output.log 2>&1 &
# 2>&1 是将标准错误重定向到标准输出，> 右边的 1 必须加 &，才表示 stdout 标准输出，不加表示文件名
```
& 是在后台运行， 当执行 ./a.out & 的时候， 即使用ctrl+c, a.out 照样运行（因为对 SIGINT 信号免疫），但是关掉 shell，进程消失。

nohup 的是忽略 SIGHUP 信号，当运行 nohup ./a.out 的时候，关闭shell, a.out 进程继续运行（对 SIGHUP 信号免疫），但用 ctrl+c 会消失。

因此，要想进程不受 shell 关闭和 ctrl+c 影响，就两个同时用

8. 服务器远程登录：
ssh -p 端口号 服务器用户名@ip ，回车后，再输入账号密码

