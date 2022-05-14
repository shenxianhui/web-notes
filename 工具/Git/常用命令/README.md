<!--
 * @Description: Git 常用命令
 * @Author: shenxh
 * @Date: 2022-05-14 11:05:47
 * @LastEditors: shenxh
 * @LastEditTime: 2022-05-14 11:10:27
-->

- [常用命令](#常用命令)
	- [用户配置](#用户配置)
	- [初始化仓库](#初始化仓库)
	- [添加文件](#添加文件)
	- [提交暂存区的文件至本地仓库](#提交暂存区的文件至本地仓库)
	- [获取远程仓库数据](#获取远程仓库数据)
	- [推送到远程仓库](#推送到远程仓库)
	- [放弃本地工作区修改](#放弃本地工作区修改)
	- [放弃暂存区的文件](#放弃暂存区的文件)
	- [查看仓库状态](#查看仓库状态)
	- [查看文件提交前后的区别](#查看文件提交前后的区别)
	- [查看历史提交记录](#查看历史提交记录)
	- [查看历史命令记录](#查看历史命令记录)
	- [克隆一个远程库](#克隆一个远程库)
	- [分支管理](#分支管理)
		- [创建一个分支](#创建一个分支)
		- [切换到指定分支](#切换到指定分支)
		- [创建并切换到指定分支](#创建并切换到指定分支)
		- [查看分支](#查看分支)
		- [推送分支](#推送分支)
		- [分支合并](#分支合并)
		- [删除本地分支](#删除本地分支)
		- [删除远程分支](#删除远程分支)
		- [查看分支合并图](#查看分支合并图)
	- [标签管理 (tag)](#标签管理-tag)
		- [创建标签](#创建标签)
		- [推送标签到远程库](#推送标签到远程库)
		- [查看标签](#查看标签)
		- [对历史提交打 tag](#对历史提交打-tag)
		- [删除标签](#删除标签)
	- [保存工作现场](#保存工作现场)
	- [回退版本](#回退版本)
	- [还原版本](#还原版本)
- [常用流程示例](#常用流程示例)
	- [推送本地代码到远程库](#推送本地代码到远程库)
	- [合并代码](#合并代码)
	- [打 tag](#打-tag)

# 常用命令

## 用户配置

```
// 设置 Git 姓名
git config --global user.name "Your Name"
// 设置 Git 邮箱
git config --global user.email "email@example.com"
```

## 初始化仓库

当前项目生成一个 `.git` 隐藏文件夹

```
git init
```

## 添加文件

提交至本地 "暂存区" (.git/index)

```
// 单个文件添加至仓库
git add <file>

// 整个目录添加至仓库, 会忽略 .gitignore 把任何文件都加入
git add *

// [常用] 整个目录添加至仓库, 会根据项目中的 .gitignore 配置文件做过滤
git add .
```

## 提交暂存区的文件至本地仓库

将已添加至暂存区的文件提交至本地 Git 仓库 (默认 master 分支)

```
// 会弹出一个 Vim 编辑器输入内容后再提交
git commit

// [常用] 直接输入内容并提交
git commit -m "在这里输入本次提交的大致内容"
```

## 获取远程仓库数据

从远程获取最新到本地, 不会合并 (merge)

```
// 将远程仓库 xxx 分支下载到本地当前分支中
git fetch origin xxx
```

从远程获取最新到本地, 并且与本地分支合并 (merge)

```
// 拉取本地已跟踪的所有远程分支
git pull

// 拉取指定远程分支
git pull origin <branch>
```

## 推送到远程仓库

```
// 将本地仓库中的代码推送至远程仓库
git push origin <branch>
```

注: 新仓库的话需要与远程库关联, 之后才能推送:

```
// 与远程库关联
git remote add origin git@github.com:xxx/git-test.git

// 删除本地库与远程库的关联
git remote rm origin
```

扩展:

有时候我们需要关联其他远程库, 需要先删除旧的关联, 再添加新的关联, 因为如果你已经关联过了就不能在关联了, 不过想关联多个远程库也是可以的, 前提是你的本地库没有关联任何远程库, 操作如下:

```
// 先关联 Github 远程库
git remote add github git@github.com:xxx/git-test.git

// 再关联码云远程库
git remote add gitee git@gitee.com:xxx/git-test.git
```

## 放弃本地工作区修改

适用于工作区修改没有 `add` 的文件

```
// 放弃指定文件的修改
git checkout -- <file>

// 放弃工作区所有文件的修改
git checkout .
```

## 放弃暂存区的文件

适用于暂存区已经 add 的文件

他会将暂存区的修改放回到工作区中

```
// 放弃暂存区指定文件的修改
git reset HEAD <file>

// 放弃暂存区所有文件的修改
git reset HEAD .
```

## 查看仓库状态

```
git status
```

## 查看文件提交前后的区别

查看工作区和版本库里面最新版本文件的区别

使用上下方向键滚动或 `Home` / `End` 键翻页, `Q` 键退出预览

```
// 指定文件
git diff <file>

// 全部文件
git diff
```

## 查看历史提交记录

查看当前分支日志

使用回车键/上下方向键滚动或 `Home` / `End` 键翻页, `Q` 键退出预览

```
git log
```

## 查看历史命令记录

查看所有分支的操作命令记录 (包括删除的记录)

使用回车键滚动

```
git reflog
```

## 克隆一个远程库

```
git clone git@github.com:xxx/git-test.git
```

## 分支管理

### 创建一个分支

```
git branch <branch>
```

### 切换到指定分支

```
git checkout <branch>
```

### 创建并切换到指定分支

```
git checkout -b <branch>
```

### 查看分支

显示的结果中，其中有一个分支前有个 \* 号，表示的是当前所在的分支

```
git branch
```

### 推送分支

```
git push origin <branch>
```

### 分支合并

指定分支与当前分支合并 (只会更新当前分支)

```
git merge <branch>
```

### 删除本地分支

```
git branch -d <branch>
```

### 删除远程分支

```
git push origin --delete <branch>
```

### 查看分支合并图

```
git log --graph
```

## 标签管理 (tag)

### 创建标签

```
git tag <tag_name>
```

### 推送标签到远程库

```
// 推送当前标签到远程库
git push origin <tag_name>

//推送所有标签到远程库
git push origin --tags
```

### 查看标签

```
// 查看标签名称
git tag

// 查看标签信息
git show <tag_name>
```

### 对历史提交打 tag

```
// 先查找历史提交的 commit id
git log --pretty=oneline --abbrev-commit

// 为指定记录打 tag
git tag <tag_name> <commit_id>

// 创建带有说明的标签
git tag -a <tag_name> -m "说明内容" <commit_id>
```

### 删除标签

```
// 1. 删除本地标签
git tag -d <tag_name>

// 2. 推送至远程
git push origin :refs/tags/<tag_name>
```

## 保存工作现场

作用：当你需要去修改其他内容时，这时候你的工作还没有做完，先临时保存起来，等干完其他事之后，再回来回复现场，再继续干活；为什么？因为暂存区是公用的，如果不通过 stash 命令隐藏，会带到其它分支去

```
git stash
```

查看已经保存的工作现场列表

```
git stash list
```

恢复工作现场 (恢复并从 `stash list` 删除)

```
// 方式1
git stash pop

// 方式2
git stash apply
```

恢复工作现场，但 `stash` 内容并不删除，如果你需要删除执行如下命令

```
git stash drop
```

恢复指定的 stash

说明：其中 `stash@{0}` 为 `git stash list` 中的一种编号

```
git stash apply stash@{0}
```

## 回退版本

在 Git 中, 用 `HEAD` 表示当前版本. 上一个版本就是 `HEAD^`, 上上一个版本就是 `HEAD^^`, 以此类推...

如果需要回退几十个版本的话可以这样写：`HEAD~50`

**注: 此方法不可逆, 回退之前建议先 `git branch tmp_branch` 创建一个备份分支, 以便恢复**

```
// 回退至上个版本
git reset --hard HEAD^

// 回退至上上个版本
git reset --hard HEAD^^

// 回退 N 个版本
git reset --hard HEAD~N
```

上述方法灵活度不高, 比较适用于回退较少的版本

如果需要回退到某个指定历史版本的话, 可以根据提交记录对应的 commit_id (版本号) 来回退

版本号就是一个使用 SHA1 计算出来的一个非常大的十六进制数字, 提交时看到的一大串类似 `6042c2cf126cf6d260a02c49a3c4453387c292a1` 的就是了

操作如下:

```
git reset --hard <commit_id>
```

不知道版本号的话可以使用以下命令查看

```
// 查看全部日志
git log -g

// 查看全部日志, 只显示版本号和提交备注, 方便阅读
git log --pretty=oneline -g
```

**注意**

到了这里, 其实只是本地回退了版本而已, 远程仓库的并没有回退

如果直接 push 到远程仓库则会报错: 提示需要执行 `git pull` 更新远程仓库

如果执行 `git pull` 的话会将刚才回退的版本下载回来

此时需要**强制**将本地代码推送至远程仓库之中:

```
git push -f origin <branch>
```

## 还原版本

回退版本后我们还可以通过以下命令还原到指定的版本

通过下面命令获取提交记录的 HEAD

查看所有分支的提交记录 (回车键滚动):

```
git reflog
```

还原到指定版本:

```
git reset HEAD@{编号}
```

# 常用流程示例

## 推送本地代码到远程库

例如当前分支为 dev

```
git add .
git commit -m "feat: 新增 xxx 功能"
git pull
git push origin dev
```

## 合并代码

例如将 dev 分支的代码合并至 master 分支

```
git checkout dev
git pull
git checkout master
git merge dev
git push origin master
```

## 打 tag

例如为当前版本打 tag: v1.0.0

```
git tag v1.0.0
git push origin v1.0.0
```
