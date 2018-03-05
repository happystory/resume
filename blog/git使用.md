由于平时工作和学习中经常会用到git，故在此记录一下。

## 重要概念
1. 已提交（committed）该文件已经被安全地保存在本地数据库中了
2. 已修改（modified）修改了某个文件，但还没有提交保存
3. 已暂存（staged）把已修改的文件放在下次提交时要保存的清单中

## 起步
初次使用需要设置姓名和邮箱
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 基本使用
```
# 创建git版本库（自动创建唯一一个master分支）
git init

# 把文件修改添加到暂存区
git add <file>
git add -A

# 把暂存区的所有修改提交到当前分支
git commit -m 'xxx'

# 查看仓库状态
git status

# 查看修改内容
git diff <file>

# 查看提交历史
git log

# 查看历史命令
git reflog

# 回退版本（HEAD表示当前版本）
git reset --hard HEAD^  
git reset --hard <commit_id>

# 撤销工作区的修改
git checkout -- <file>

# 撤销暂存区的修改
git reset HEAD <file>

# 从版本库删除文件
git rm <file>
```

## 远程仓库
```
# 查看远程仓库信息
git remote -v

# 添加一个远程库的标签
git remote add origin git@xxx.git

# 推送到origin标签的地址上
git push origin master

# 慎用，这样会强制推送，会覆盖别人的代码
git push -f origin master

# 删除origin标签
git remote remove origin

# 修改origin标签对应的地址
git remote set-url origin git@xxx.git

# 把origin 改成 coding
git remote rename origin coding

# 从远程库克隆
git clone git@xxx.git

# 给fork添加源库clone地址
git remote add upstream git@xxx.git

# 从上源仓库 fetch 分支和提交点，并会被存储在一个本地分支 upstream/* 而不是origin /*
git fetch upstream

# 把 upstream/分支 合并到本地对应的分支上
git merge upstream/master

# push
git push origin master
```

## 分支操作
```
# 查看分支
git branch -a（蓝色本地，红色远程）

# 创建本地库dev分支
git branch dev

# 切换到dev分支
git checkout dev

# 创建并切换分支
git checkout -b dev

# 把dev分支上的内容合并到当前分支上
git merge dev
git merge --no-ff -m "merge with no-ff" dev （禁用Fast forward）

# 删除分支
git branch -d dev
git branch -D dev （强制删除）

# stash
git stash
# 查看stash
git stash list
# 恢复stash
git stash apply
git stash apply stash@{0}
# 删除stash
git stash drop
# 恢复并删除stash
git stash pop

# 抓取远程的新提交
git pull

# 在本地创建和远程分支对应的分支
git checkout -b dev origin/dev

# 建立本地分支和远程分支的关联
git branch --set-upstream dev origin/dev
```

## 标签管理
```
# 打标签
git tag <name>
git tag <name> <commit_id>
git tag -a <name> -m 'xxx' <commit_id>

# 查看标签
git tag

# 查看标签信息
git show <tagname>

# 推送某个标签到远程
git push origin <tagname>

# 推送全部未推送过的本地标签
git push origin --tags

# 删除本地标签
git tag -d <tagname>

# 删除远程标签 
git push origin :refs/tags/<tagname>
```

## 常见问题
1. git add -A与git add .的区别
 ```
git add -A  提交所有变化
git add -u  提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)
git add .  提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件
```

2. 关于`Fast forward`模式
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

3. 与fork仓库与源库同步
https://help.github.com/articles/syncing-a-fork/