## mac 环境变量存储
Mac 系统下的环境变量存在的地方：
/etc/profile 
/etc/paths 
~/.bash_profile
~/.bash_login 
~/.profile 
~/.bashrc 
~/.zshrc

1. /etc/profile 和 /etc/paths 是系统级别的，系统启动就会加载。其他五个是当前用户级的环境变量。
2. ~/.bash_profile, ~/.bash_login, ~/.profile 按照从前往后的顺序读取，如果 ~/.bash_profile 文件存在，则后面的几个文件就会被忽略不读了，以此类推。
3. mac 中是 ~/.bash_profile，linux 中是 ~/.bashrc，且不受上述规则限制，~/.bashrc 是 bash shell 打开时载入的
4. ~/.zshrc 是安装了 zsh，需要在该文件中配置环境变量

## 修改环境变量
mac 一般在 ~/.bash_profile 中添加环境变量，修改系统级变量时在 /etc/profile 中进行修改。

1. 设置 PATH 语法：
```sh
export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>
```

2. 修改完成后，执行 source ~/.bash_profile，环境变量则立即生效

## 安装 zsh 配置环境变量
修改了 ~/.bash_profile 文件但发现环境变量没有生效，并且提示 zsh: command not found: homestead，这是因为安装了 zsh 后 ~/.bash_profile 文件不会被执行，可以将进行如下配置：
1. vim ~/.zshrc 
2. 在 ~/.zshrc 文件中添加 source ~/.bash_profile
3. source ~/.zshrc , 这样 ~/.bash_profile 配置的环境变量同样有效，因此之后也只需要在 ~/.bash_profile 文件中添加环境变量即可。

## maven 需要添加的环境变量
```sh
export M2_HOME=【maven目录】
export M2=$M2_HOME/bin
export PATH=$M2:$PATH
```

## android 相关
```sh
export ANDROID_HOME=【android目录】
PATH=${PATH}:$ANDROID_HOME/platform-tools
PATH=${PATH}:$ANDROID_HOME/tools
```