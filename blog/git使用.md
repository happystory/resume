# git使用

## 重要概念
1. 已提交（committed）该文件已经被安全地保存在本地数据库中了
2. 已修改（modified）修改了某个文件，但还没有提交保存
3. 已暂存（staged）把已修改的文件放在下次提交时要保存的清单中

## 起步
初次使用需要设置姓名和邮箱
```
git config --global user.name "姓名"
git config --global user.email xx@qq.com
```

## git commit -m 与 git commit -am区别
当修改已经通过git add <change file>将其添加到stage，可以通过git commit -m "<message>"为这所有已经进入stage的改变添加一个commit信息。可以直接使用git commit -am "<message>"，将所有修改，但未进stage的改动加入stage，并记录commit信息。

## 远程仓库操作
```
# 查看远程仓库信息
git remote -v

# 慎用，这样会强制推送，会覆盖别人的代码
git push -f origin master

# 添加一个远程库的标签
git remote add origin git@xxx.git

# 推送到origin标签的地址上
git push origin master

# 删除origin标签
git remote remove origin

# 修改origin标签对应的地址
git remote set-url origin git@xxx.git

# 把origin 改成 coding
git remote rename origin coding
```

## 分支操作（重要）
```
# 查看分支
git branch -a（蓝色本地，红色远程）

# 创建本地库dev分支
git branch dev

# 切换到dev分支
git checkout dev

# 把dev分支上的内容合并到当前分支(master)上
git merge dev
```

由于一些常用的命令诸如`git add`或者`git commit`等平时使用较多，比较熟悉，就不重复了。