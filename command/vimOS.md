# vimOS
介绍纯键盘操作的一套软件

## 目录
[TOC]

## i3wm
### 安装与启动
arch系: `sudo pacman -S i3`

启动使用`exec i3` 或者在原有登录器(如果有)中选择桌面系统  
初次启动可以选择使用的\$mod键([配置](#配置))
重置配置可以使用`i3-config-wizard`

### 其他软件
`sudo pacman -S dmenu-run` *i3-dmenu-run* 基于此 可用于快速启动软件

### 配置
***配置文件目录: `~/.config/i3/config`***

> 类似vim配置  

`set $<var> <value>` 设定变量 如\$mod一般为Mod1/Mod4(见下表) 作为i3中的特殊按键 默认绝大多数i3按键都用到了`$mod+其他按键`的操作方式  

`bindsym <key><orginKey>` 按键映射  
注意如果多个映射对应了单个按键 将会在加载配置文件时报错 请注意避免冲突

| 特殊按键  | 对应实际按键 |
| :-------- | ------------ |
| Mod1      | Alt          |
| Mod4      | Win/Super    |
| Left      | 方向左       |
| Down      | 方向下       |
| Up        | 方向上       |
| Right     | 方向右       |
| Return    | 回车         |
| Escape    | Esc          |
| Control   | Ctrl         |
| semicolon | 分号         |

以下命令大多配合`bindsym`使用:

`exec <command>` 执行终端命令 配合`bindsym`可做到如一键打开软件的效果, 例:
`bindsym $mod+c google-chrome-standed` 使用`$mod+c`一键开启chrome浏览器
其他命令可直接参考配置文件

### 一般
**以下均在默认配置下结合建议映射进行说明:**  

一共默认用到的按键:
`$mod` `Shift` `wes` `f` `vh` `jkl;` `Return` `d` `1234567890` `q`

- `exec i3-sensible-terminal` 默认为`$mod+Return`  
`i3-sensible-xxx`为i3wm的默认启动软件 这里为终端(terminal)  
具体启动的终端将按一定顺序查找 可以自行更改该行配置 启动其他终端  
推荐习惯ctrl+alt+t开启终端的用户在配置文件中添加映射  
例:  
`bindsym $mod+Return exec konsole`, `bindsym Control+Mod1+t exec konsole`

- `focus left/down/up/right` 默认为`$mod+j/k/l/;`  
切换聚焦窗口 也可以使用鼠标 移动到对应窗口会自动切换 而非常见桌面环境的点击聚焦
```
    l
    ^
    |
j<--+-->;
    |
    V
    k
```

`j` `k` `l` `;`分别同左下上右方向键 相比vim 更照顾一般的打字右手闲置位置  
对于vim用户 更推荐更改配置文件以符合操作习惯:  

```
bindsym $mod+h focus left
bindsym $mod+j focus down
bindsym $mod+k focus up
bindsym $mod+l focus right
...
bindsym $mod+Shift+h move left
bindsym $mod+Shift+j move down
bindsym $mod+Shift+k move up
bindsym $mod+Shift+l move right
...
bindsym $mod+v split toggle      # 避免按键冲突 并且更改为操作逻辑为切换 具体作用见下
# bindsym $mod+semicolon split h
# bindsym $mod+v split v
```

- `split h/v` 默认为`$mod+h/v`  
更改**此后创建的**窗口的分屏方式 分别指vertical(垂直) horizontal(水平)  
> 推荐改为`... split toggle` 变为单个按键进行垂直和水平分屏间切换

- `kill` 默认为`$mod+Shift+q`  
关闭窗口 如大多数软件的`ctrl+w`以及一般桌面环境窗口右上角的关闭键

- `fullscreen toggle` 默认为`$mod+f`  
当前窗口全屏

- `layout stacking/tabbed/[toggle split]` 默认为`$mod+s/w/e`  
调整当前工作页的窗口管理方式  
1. *stacking* 为堆叠模式 多个窗口将堆叠起来 只有当前聚焦窗口独占整个工作页  
2. *tabbed* 为标签页模式 类似堆叠模式 但操作上更像浏览器标签页 仅表示方式不同  
3. *toggle split* 为平铺模式 默认模式 类似vim的分屏 保持只要有窗口 屏幕将必添满窗口
> 可改为`... split toggle` 变为单个按键进行模式间切换

*默认配置:*
```
bindsym $mod+s layout stacking
bindsym $mod+w layout tabbed
bindsym $mod+e layout toggle split
```

- `floating toggle` 默认为`$mod+Shift+space`  
将当前窗口调整为浮动 相当于普通桌面环境的一般小窗口  

- `workspace number <number>` 默认为`$mod+数字`  
切换工作页 注意多屏下每个屏幕都是一个工作页

- `move container to workspace number <number>` 默认为`$mod+Shift+数字`  
将当前窗口移动至指定工作页

- `mode "resize"` 默认为`$mod+r`  
进入resize模式 可使用方向键或`jkl;`调整窗口尺寸  
上: 减少垂直尺寸; 下: 增加垂直尺寸  
左: 减少水平尺寸; 右: 增加水平尺寸  
注意 与vim一样 **调整尺寸的按键方向与窗口的位置无关**


### 调试

- `reload` 默认为`$mod+Shift+c`  
重新加载i3wm配置文件

- `restart` 默认为`$mod+Shift+r`
重新启动i3wm

- `exec i3-msg exit` 默认为`$mod+Shift+e`
关闭i3wm 配置中并非只有这句 还添加了弹出确认框


### 参考链接
https://www.bilibili.com/video/av55390167  
https://www.jianshu.com/p/99e51eb15abc

