# HardDisk
硬盘工具  

#### 调整硬盘前请尽可能做好备份 并且在执行前三思!!!

## 目录
[TOC]

## 文档规则说明
因为markdown面向html 因此所有非 `代码框`(\`原文\`)内的小于号都改为了 `\\<` 如果看到请自行忽略转义符 `\`(反斜杠)  

\<string1/string2> 使用string1或string2代替 更多"/"时同理(如"\<file>"指使用文件名代替)  

\<Disk> 硬盘路径 一般为`/dev/sdxx`(sata) 或 `/dev/nvmenxpx`(nvme)  
第一个x为硬盘序号(sata为英文序号 从a开始, nvme为数字 从0开始), 第二个x为分区序号  
如: /dev/sdb5 (2号sata硬盘的第5分区), /dev/nvmen0p1 (1号nvme硬盘的第一分区)

\[c0/c1/c2\] 可选 一般指代按键枚举值

> 注意这与vim配置描述格式并不一样 更贴近人类可读性(如"on/off"指输入on或off代替)  

"默认" 指代不进行输入时的结果  

## 硬盘部分知识点

- 分区表

目前主流分mbr与gpt(GUID) 引导进入系统有所区别  
此外mbr不支持大于2T的硬盘 以及最大支持4个主分区(更多需要使用逻辑分区)

| 类型 | 最大硬盘大小 (512B/扇区)   | 最大主分区数量 |
| --- | --- | ---- |
| MBR | 2TiB | 4 (需要更多分区则需依靠逻辑分区) |
| GPT | 64ZiB | 128 |

- 引导类型

引导系统分 legacy(bios) 与 uefi, uefi启动一般更快  
1. 目前(2020年)所有电脑都应该是uefi引导 兼容传统bios  
2. uefi引导需要efi分区  
3. 一般来说分区表类型与引导系统应该是: legacy\<->mbr, uefi<->gpt 向下兼容 但也可以互换

- 文件系统

目前主要有:
| 类型 | 常用系统 | 缺点 |
| --- | --- | ---- |
| fat16/fat32 | 通用 bios/uefi也可直接引导 | 单文件最大4G 成为既最适合作为系统安装iso又最有局限性的文件系统 |
| ntfs | windows | 其他系统支持不一 大多有软件使用限制 |
| ext3/ext4 | linux | windows下支持极差 |
| exfat | 通用 | 兼容性稍好 但相比fat16/fat32 uefi无法进行直接引导 |
格式化时务必考虑清楚使用的文件系统类型  

此外还有linux-swap 是linux系统的缓存交换分区

- 分区标识

主要有:
1. boot(可引导)
2. esp(uefi可引导)
3. bios-grub(grub系统引导器)
4. swap(交换分区)
5. msftdata(windows分区)
6. msftres(windows恢复分区)
7. hidden(隐藏)

## fdisk
命令行软件 大多环境都有预装 建议至少了解使用  
此外 fdisk有汉化版

- 使用

`fdisk <disk>` 需要root, \<disk>选择硬盘进行编辑  
`-l` 列出所有硬盘及其分区 不需要\<disk>

- 帮助信息
```
更改将停留在内存中，直到您决定将更改写入磁盘。
使用写入命令前请三思。


命令(输入 m 获取帮助)：m

帮助：

  GPT
   M   进入 保护/混合 MBR

  常规
   d   删除分区
   F   列出未分区的空闲区
   l   列出已知分区类型
   n   添加新分区
   p   打印分区表
   t   更改分区类型
   v   检查分区表
   i   打印某个分区的相关信息

  杂项
   m   打印此菜单
   x   更多功能(仅限专业人员)

  脚本
   I   从 sfdisk 脚本文件加载磁盘布局
   O   将磁盘布局转储为 sfdisk 脚本文件

  保存并退出
   w   将分区表写入磁盘并退出
   q   退出而不保存更改

  新建空磁盘标签
   g   新建一份 GPT 分区表
   G   新建一份空 GPT (IRIX) 分区表
   o   新建一份的空 DOS 分区表
   s   新建一份空 Sun 分区表
```

## cfdisk
与fdisk同样是命令行 但为类gui的操作逻辑 更容易操作
同样有中文版

- 安装

debain系: `sudo apt install cfdisk`  
arch系: `sudo pacman -S cfdisk`

- 使用

不需要参数 直接使用`cfdisk`即可 方向键高亮选项 回车键确定 `q`键直接退出

## gparted
gui界面 不介绍使用方法  
更改硬盘需要安装gpart  

- 安装

debain系: `sudo apt install gparted gpart`  
arch系: `sudo pacman -S gprated gpart`

