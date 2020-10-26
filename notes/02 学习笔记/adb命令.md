### adb 工作原理
1. 启动 adb 客户端时，客户端首先检查是否有 adb 服务器进程正在运行。若没有，客户端将启动服务器进程。

2. 服务器启动后与本地 TCP 端口 5037 绑定，并监听 adb 客户端发出的命令，所有 adb 客户端均通过端口 5037 与 adb 服务器通信。

3. 服务器与所有正在运行的设备建立连接。它通过扫描 5555 到 5585 之间（该范围供前 16 个模拟器使用）的奇数号端口查找模拟器。服务器一旦发现 adb 守护进程 (adbd)，便会与相应的端口建立连接。注意：每个模拟器都使用一对按顺序排列的端口，用于控制台连接的偶数号端口和用于 adb 连接的奇数号端口。在端口 5555 处与 adb 连接的模拟器与控制台监听端口为 5554 的模拟器是同一个。
模拟器 1，控制台：5554
模拟器 1，adb：5555
模拟器 2，控制台：5556
模拟器 2，adb：5557

4. 服务器与所有设备均建立连接后，则可使用 adb 命令访问设备。

### 常用adb命令
adb devices 查看当前连接设备； adb devices -1 将输出设备信息，用于区分设备
adb kill-server 重置 adb 主机
adb connect device_ip_address 通过 ip 连接到设备，如果 adb devices 找不到设备，可以通过此命令进行连接，如连接本机模拟器 adb connect 127.0.0.1:5555

### adb shell
android 是基于 linux 系统开发的，因此也支持常用的 linux 命令，可以通过 adb shell 来执行 linux 命令。
adb shell 用于进入手机或模拟器的 shell 内核，电脑连上手机后需要打开手机的调试模式才可以使用。

#### dumpsys
dumpsys 是一种在 android 设备上运行的工具，可以提供有关系统服务的信息，使用 adb shell dumpsys 获取设备的所有系统服务的诊断输出。

adb shell dumpsys window: 查看 window 相关信息
adb shell dumpsys activity: 查看 activity
adb shell dumpsys activity | grep mFocusedActivity： 查看当前顶部 activity

['/Applications/PyCharm.app/Contents/plugins/python/helpers/pydev', '/Applications/PyCharm.app/Contents/plugins/python/helpers/pycharm_display', '/Applications/PyCharm.app/Contents/plugins/python/helpers/third_party/thriftpy', '/Applications/PyCharm.app/Contents/plugins/python/helpers/pydev', '/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.7/lib/python37.zip', '/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.7/lib/python3.7', '/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.7/lib/python3.7/lib-dynload', '/Users/xieyiyu/Library/Python/3.7/lib/python/site-packages', '/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.7/lib/python3.7/site-packages', '/Applications/PyCharm.app/Contents/plugins/python/helpers/pycharm_matplotlib_backend', '/Users/xieyiyu/Projects/pyrig']
