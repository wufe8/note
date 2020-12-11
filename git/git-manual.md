# git
## 目录
[TOC]
## 获取仓库

`git init` 创建仓库

`git clone [url] [path]` 拷贝项目 到指定目录(可选)

## 提交内容
`git add [file]`添加文件 写入缓存区  

`git rm [file]`删除缓存区，版本区，本地文件 --cached 只删除缓存区文件(推荐) -r 允许删除文件夹

`git commit` 提交到仓库并备注信息 -a 不备注 -m 简易备注 后加[string] (`git commit -am` 直接提交 但不推荐)
	--amend 重新上传最近上传

## 检查历史
`git status [path]` 查看修改 默认仓库根目录(无论在仓库哪里) -s简短输出

`git diff` 查看详细修改信息 未缓存 --cached查看已缓存改动 HEAD查看所有 --stat仅摘要

`git log` 查看提交历史 --oneline简洁输出 --graph 查看出现分支 --reverse 逆向日期显示(从老到新) --all 全部分支  
	--auther=[name]查看指定用户 --since --before --until --after [date]日期范围 --decorate查看标签
推荐`git log --oneline --graph --all`

## 分支管理 
- `git branch [name]`  
  添加分支 不填显示分支清单(本地) -d [name]删除分支

- `git checkout [name]`  
  切换分支

- `git tag`  
  查看所有标签 -a 创建不带注解 日期 创建人的标签  
  +[etc] 创建标签 [finger]追加标签到历史提交

- `git reset [type] HEAD`  
  撤销commit [type]即: --mixed不删除工作改动 撤销commit,add
  --soft不删除工作改动 撤销commit 
  --hard 删除工作改动 撤销commit,add (=回放上次commit)

- `git merge [alias] [branch]`  
  提取并合并到[branch]分支 后加[to]指定提取[to]branch 默认当前branch

- git rebase [branch] [long]  
  类merge 但直接拉至目前branch下 HAND指向最后更新 [long]长度  
  -i 自定义管理  
  ^* 上1个的第*分支branch 默认1 ~* 上*的branch 默认1

- git cherry-pick [branch1] [branch2]...  
  将[branch*]提取到当前分支下 HAND指向最后更新

## 远程管理
- `git remote add [alias] [ssh/https]`添加远程仓库 注:[alias]填远程别名 一般可填origin

- `git remote`查看当前配置的仓库 -v 实际地址 rm [alias] 删除

- `ssh-keygen -t rsa -C "xxx@email.com"`生成ssh key

- `git push [alias] [branch]`  
  提交文件 -f 替换文件  
  \[from]:[to]将[to](远程)中不同的用[from](本地)的替换 [from]为空同理 为删除

- `git fetch` 下载新分支及数据

- `git pull [alias] [branch]`
  同git fetch ;git merge 下载并合并 [...]  
  \[from]:[to]类push 注意[from](远程) [to](本地) 若[from]为空 则自动创建远程分支


## 例子-创建仓库并提交
git init
git add *
git commit -m "..."
git remote [link]
git pull origin master

## 配置
- 设置名字与邮箱:
```
git config --global user.email [email]
git config --global user.name [name]
```
- 别名例子:  
`git config --global alias.lg "log --oneline --graph --all"`

## 笔记贡献者
wufe8
