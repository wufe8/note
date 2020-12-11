# Linux 常用文件

## 文件结构
/etc/fstab 开机自动挂载硬盘
~/.ssh ssh配置
~/.vim vim插件
.vimrc vim配置
~/.config/ibus ibus输入法系统配置
~/.config/nvim neovim插件
~/.config/nvim/init.vim neovim配置
/etc/profile 全局变量
~/.bashrc 个人bash变量
/usr/share/fonts 系统字体
~/.local/share/fonts 个人字体
~/.local/share/applications 个人软件
/etc/init.d/... 开机启动 需更新
/etc/profile.d/*.sh 登录执行

## .desktop文件模板
```
[Desktop Entry]
Encoding=UTF-8
Name=SomethingInteresting
Comment=idk what interesting actrully.
Exec=~/test.sh
Icon=~/icon64.png
Terminal=false
StartupNotify=true
Type=Application
Categories=Application;Development;
```
