# console  

ctrl+alt+t 呼出命令行(linux)  

`man [command]` 帮助  

> 部分命令并非来自(部分发行版的)自带软件 关于安装 请查看[包管理器](#包管理器)
> 关于常用软件 可以查看my-linux仓库中的init.txt

## 导览
- [进程与服务](#进程与服务)
- [用户权限](#用户权限)
- [文件管理](#文件管理)
- [文件权限](#文件权限)
- [压缩文件](#压缩文件)
- [磁盘管理](#磁盘管理)
- [网络](#网络)
- [包管理器](#包管理器)

## 进程与服务
`ps` 查看当前终端的所有进程  
`-a` 查看当前设备的所有终端的进程
`-x` 显示所有进程 不区别设备与终端  
`-u` 以用户为基准进行显示  
`-e` 或 `-A` 显示所有进程  

`ps -aux` 推荐配合 [grep](#正则表达式\(regular-expression\)) 使用

`top` 一款可以实时查看并更新进程状态的终端程序

`kill [threadNumber]` 杀死进程 通常配合`ps -aux`使用

`service [name] [action]`服务管理
[action] 有start stop reload force-reload status 顾名思义

## 用户权限  
`sudo [command]` 以root权限执行 需要有权限 并输入使用成员密码  
`su [user]` 登陆[user] 默认root用户 需要输入密码 root除外  
`passwd [user]` 修改[user]密码 需要输入原密码 root除外  
`exit` 退出账户(通用)  
`logout` 退出连接(ssh等远程连接使用)  

## 文件管理  
.为当前文件夹 ..为父文件夹  

`pwd` 当前位置  

`ls [pos]` 文件列表  
`dir [pos]` 同上(windows cmd only)  
`-l` 详细列表 (ll即ls -l)  
`-a` 所有文件(包括.开头的隐藏文件)  
`-h` 自动判断使用单位(k m g t)  

- exp  

```
total 5  
drwxr-xr-x  1 Wufe8 Wufe8   0 3月 29 00:35 ./  
drwxr-xr-x  1 Wufe8 Wufe8   0 4月  7 01:11 ../  
--rw-r--r-- 1 Wufe8 Wufe8 442 3月 28 20:58 dos.txt  
--rw-r--r-- 1 Wufe8 Wufe8 280 3月 28 20:56 vim.txt  
drwxr-xr-x  1 Wufe8 Wufe8   0 3月 28 21:12 新建文件夹/  
权限         所有者 所有组 大小 创建日期    文件(夹)名字 
```

`chown [name] [owner]` 修改文件(夹)所有者 需要为root用户或者所有者  
-R 递归 即包含子文件(夹)  
`chgrp [name] [group]` 修改文件(夹)所有组 需要为root用户或者所有者  
-R 递归 即包含子文件(夹)  
`chmod [number3] [name]` 修改文件(夹)权限 需要为root用户或者所有者  
或者 chmod [u/g/o/a][+/-/=][r/w/x] [name] 可用逗号分隔 如chmod u+wx,g+w,a+r dos.txt  
u=user 所有者 g=group 所有组 o=other 其他成员 a=all 所有  
-R 递归 即包含子文件(夹)  

## 文件权限  
`-rwxrwxrwx`  
第1位为文件类型 -为普通文件 d为文件夹  
2-10位为权限 r 可读 w 可写 x 可执行 -没有权限 不存在留空  
前3位为所有者权限 中3位为所有组权限 后3位为其他成员权限  
一般root用户不受影响 无视权限  
`[number3]` 即二进制化 **r=4 w=2 x=1** 3位分别对应3成员  

- exp:  

原为 -rw-------  
chmod 754 dos.txt 或者chmod u=rwx,g=rx,o=r dos.txt  
修改./dos.txt文件的权限为:所有者可读,写,执行 所有组可读,执行 其他成员只读  
即: -rwxr-xr--  

----------------------

`find [pos]` 文件列表及其子目录文件列表  

`cd [pos]` 移动目前位置(相对or绝对)  
(linux中默认为~ 即用户目录)  

`mkdir [name]` 创建文件夹  

`rmdir [name]` 删除文件夹  

`touch [name]` 创建文件  

`echo [string]` 输出字符串 >> [file]重定义 写入至文件  

`cat [file]` 输出文件内容  
`tac [flie]` 倒置输出文件内容(tac就是cat倒写)  

`list [flie]` 输出文件内容 但内嵌窗口 可上下滑动 q退出  

`rm [file]` 删除文件  
`del [file]` 删除文件  
-r 递归 -f 不询问直接删除  

`mv [file] [pos/rename]`移动文件or重命名文件  

### 正则表达式(regular expression)
`grep [string]`  

## 压缩文件  
- .tar.gz 
> 含义: .tar打包 .gz压缩  

`tar [name] [target]` 打包  
-c 产生新包  -r 添加文件到包中 -u 更新包中文件(update) -f 指定包文件名(file)  
-z 压缩(产生.gz 等同于gzip [name] [target])(gzip)  
-x 解压(extract) [target]后接-C [pos] 指定位置(可选 默认为所在目录)  
-v 详细信息(verbose)  

- 简单来说: 

`tar -zcvf [name] [target]` 压缩[target]到[name]  
`tar -zxvf [name] -C [pos]` 解压[name]到[pos](-C [pos] 可选 默认为所在目录)  

`tar [name]` 包动作  
-x 列出包内文件  
`gzip [name] [target]` gzip压缩(产生.gz)  
-d 解压到[target]  

`zip [name] [target]`压缩zip  
`unzip [name]`解压zip  

## 磁盘管理  
`df` 列出挂载磁盘信息  
`fdisk` 列出各分区信息  

更多请见[HardDisk.md](../command/HardDisk.md)  

## 系统  
`shutdown [time]` 关机 root限定  
`-r` 重启(同reboot) `-c` 取消  
[time]可选单位 默认分钟(windows默认为秒) now为立刻(同halt) hh:mm准确时间  
`halt`或 `-n` 立刻关机 root限定  
reboot [time] 重启 root限定  

> 如果在gui桌面下输入 那么不要求为root用户

`sudo update-rc.d [file] defaults 90` 将指定文件加入系统启动项  

`hostnamectl` 系统信息  
`hostnamectl set-hostname [name]` 更改电脑名称  

## 配置
`xrandr` 列出显示设备信息 --help 帮助
--output 指定设备 --mode 设置分辨率 --rate 设置刷新率
> 设置刷新率可能需要同时设置分辨率
`arandr` 简易gui的xrandr

`volumeicon` 状态栏增加音量调节按钮
`mate-power-manager` 电源管理
`feh --bg-fill [path]` 设置壁纸 多屏幕则按照顺序 用空格分割 分别指定路径

`kbdrate` 键盘自动重复输入(即按住按键自动连点的功能)
`-r [int]` 调节自动输入速度 `-d [int]` 调节自动输入需要的最低按住时长
`atkbd.softrepeat=1` 在内核命令行中添加可解除以下限制: 最低250ms delay 以及 最大30cps

## 网络  
`ifconfig` 输出ip信息  
`ipconfig` 同上(windows cmd only)  
`ping` [ip] 发送网络包以检查延迟,丢包率  

`curl [url]` 下载链接  

`ip addr` 或 `ip link` 检查网卡接入情况  

> [参考来源](https://segmentfault.com/a/1190000022751690)  

`pppoeconf` 拨号连接配置  
`pon dsl-provider` 手动连接  
`poff dsl-provider` 手动断开  
`plog` 查看状态  

关于网络连接 从易用性来看 推荐NetworkManager
- 配置  

打开`/etc/NetworkManager/NetworkManager.conf`
将第五行false改为true 即可默认启动nwm
```
4 [ifupdown]
5 managed=true
```

- 使用
`nm-connection-editor`  gui操作 最简单  
`nmtui` 文字ui操作 推荐使用  
`nmcli` 终端指令操作  

## 包管理器
- debian系  
`dpkg [app]` 目标为.deb 本地安装  
`-i` 安装软件包 `-r` 删除软件包 `-P` 删除软件包同时删除配置文件 `-L` 显示软件包关联文件 `-l` 显示已安装软件包列表  

`apt [command] [name]` 远程仓库安装  
install remove顾名思义  
或者: `apt-get` 类似`apt` 但较老  

- redhat系安装软件包  
`yum`  
`rpm`  

- arch系安装软件包
`pacman [app]`  
`-S` sync 安装 `-R` remove 卸载 `-U` upgrade 升级  
`-Syy` 更新aur(arch用户仓库) `-Syu` 滚动更新软件包  
