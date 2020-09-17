---
title: git command
date: 2020-09-18 01:15:49
tags:
---



## branch

- 创建分支

```bash
git	branch	[name]
```

- 切换分支

```bash
git	checkout	[branch name]
```



- 创建以及切换分支

```bash
git	checkout	-b	[branch name]
```



- 删除分支

```bash
git	branch	-d	[branch name]
```



- 强制删除分支

```bash
git	branch	-D	[branch name]
```



- 查看分支

```bash
git branch
```



- 查看所有分支(包括远端)

```bash
git branch -a
```



- 恢复已经删除的branch

```bash
git branch [branch name] commit-id
```



- 查看已经合并过的分支

```bash
git branch --merged
```



- 查看没有合并过的分支

```bash
git branch --no-merged
```



- 查看已经合并的分支，且排除|master|develop|skip_branch_name这些分支

```bash
git branch --merged | egrep -v "(^\*|master|develop|skip_branch_name)"
```



- 查看已经合并的分支，且排除|master|develop|skip_branch_name这些分支,并且删除筛选出来的分支

```bash
git branch --merged | egrep -v "(^\*|master|develop|skip_branch_name)" | xargs git branch -d
```



- 查看没有合并的分支，且排除|master|develop|skip_branch_name这些分支,并且删除筛选出来的分支

```bash
git branch --no-merged | egrep -v "(^\*|master|develop|skip_branch_name)" | xargs git branch -D
```


- 远端存在dev分支，本地不存在该分支,下面命令可以在本地创建一个和切换dev分支

```bash
git checkout dev
```


- 在本地删除远端分支

```bash
git push origin --delete dev
```

## commit

- 提交已经add的所有文件记录到history

```bash
git commit -m "message"
```



- 先执行(add .),把所有改动文件加入到stage,然后提交到history

```bash
git commit -am "message"
```



- 这样提交会进入[unix]风格的message编辑器
  - 按insert进入编辑状态
  - 编辑完成按ctrl C退出编辑状态
  - 输入:wq保存且退出
  - 输入:q不保存且退出

```bash
git commit
```


- 修改最近一次提交的msg

```bash
git commit --amend
```

- 修改最近一次提交(把忘记提交的文件加到这次提交里面)，并且不修改提交msg

```bash
git commit --amend --no-edit
```





## repo

- 创建repo_name文件夹，以及创建一个仓库(生成.git文件夹)

```bash
git init repo_name
```



- 删除.git目录

```bash
rm -rf .git
```


- 迁移仓库到新的仓库
  1. 在本地仓库链接要迁移的仓库地址
  2. 把本地仓库内容push到新的仓库

```bash
git remote set-url origin new_repo_url

git push --all
```

## cat

- 查看HEAD指向

```bash
cat .git/HEAD
```

- 查看文件

```bash
cat file_name
```

## diff

- 显示工作区文件的前后对比

```bash
git diff file_name
```

- 显示文件在工作区以及暂存区的变化

```bash
git diff HEAD --file_name
```


## conflict

fix conflicts and then commit the result

- 查看冲突

```bash
git status
```



- 忽略合并

```bash
git merge --abort
```



## log

```bash
git log
```



```bash
git log --oneline
```



```bash
git log --oneline --graph
```



- 最左侧是最新条件版本的history

```bash
git log --oneline --graph --all
```




- 查看最近提交的2个commit版本路线图

```bash
git log --oneline --graph -2
```


- 显示所有并且是完整的commit-id

```bash
git log --pretty=oneline
```

## fast-forward

- 不使用fast-forward(快转机制)
  1. 要合并的branch_name跟与之合并的branch中有相同名称文件,并且相关文件内容不一样,会触发fast-forward
  2. 不使用fast-forward会保存所有提交

```bash
git merge branch_name --no-ff
```


- 禁用fast-forward模式，提交merge的commit信息(如果这时删除branch_name分支，合并后的master分支里面关于branch_name的commit信息丢失)

```bash
git merge --no-ff -m "merge branch_name" branch_name
```


- 默认使用fast-forward
  1. master要合并develop分支，合并后与develop一致(内容一致)
  2. develop最新commit将不会显示在版本路线图中  

```bash
git merge [branch name]
```


## reset

- 删除暂存区所有文件;删除指定文件(在工作区文件内容不受影响)

```bash
git reset HEAD

git reset HEAD file_name
```

- 回滚到某次提交,history上在commit-id之后提交的记录都被删除(在commit-id提交之后所有修改内容都会在工作区得到保留)

```bash
git reset commit-id

git reset --mixed commit-id
```

- 回滚到某次提交，在这个提交之后的所有修改都会被删除;(工作区)

```bash
git reset --hard commit-id
```


## revert

- 恢复对应commit-id提交的所有内容(commit-id所有修改被删除),新增一个commit记录(相当于回退到某个版本,而放弃该版本之后的所有修改)

```bash
git revert commit-id
```


## merge

- 恢复到合并前的状态

```bash
git reset --hard ORIG_HEAD
```

- 合并branch_name到当前分支

```bash
git merge branch_name
```

{%asset_img merge.svg%}


- 合并branch,但是先不提交commit(可以先测试合并是否成功),再考虑提交合并commit

```bash
git merge [branch name] --no-ff --no-commit
```




- 压缩branch_name的commit(在合并后的branch里面不显示branch_name的commit)

```bash
git merge --squash [branch name]
```


## checkout 

1. 使用暂存区file_name去覆盖工作区file_name(删除工作区的所有修改)
2. 如果file_name已经存在暂存区，而工作区file_name被删除了，这个命令也可以将暂存区file_name恢复到工作区(内容是暂存区内容)

```bash
git checkout file_name
```

- 回滚到某个版本
  1. 使用:one:创建一个新的branch去保存删除的commit，并切换到新的branch
  2. 使用:two:撤销回滚版本这个操作

```bash
git checkout commit-id
```

:one:

```bash
git switch -c <new-branch-name>
```

:two:

```bash
git switch -
```

- 回滚某个文件到指定版本(这个版本之后的所有修改丢弃)(history的所有提交记录不会被删除)

```bash
git checkout commit-id -- file_name
```

- 所有文件回滚到指定版本(这个版本之后的所有修改丢弃)(history的所有提交记录不会被删除)

```bash
git checkout commit-id -- .
```

## push

- 两条命令相同

```bash
git push --set-upstream origin master

git push -u origin master
```




- 上传所有分支到远端

```bash
git push --all
```

## rebase

- feature分支重新基于master分支

```bash
git rebase master
```

{%asset_img rebase.svg%}


- 重新打开rebase编辑界面

```bash
git rebase --edit-todo
```


- 以交互式方式修改历史(-i: 交互);这里会呈现最近3个提交,它们显示的顺序是与提交顺序相反;如果对最远端(历史最久的第三个)的提交进行修改，那么它之后的所有提交的commit-id都将发生改变

```bash
git rebase -i HEAD~3
```

- 仅仅提供修改commit信息,不会影响文件内容(如果reword的是第一个(反序显示),那么之后增加的所有文件不可见(不能修改))

```bash
# r, reword <commit> = use commit, but edit the commit message
```

- 在这个模式下可以修改这次以及之前提交的文件,或者新增文件,不会影响后面的文件内容

```bash
# e, edit <commit> = use commit, but stop for amending
```

- 合并选中commit以及这条commit之前的commit(相关提交改动的内容没有变化)

```bash
s, squash <commit> = use commit, but meld into previous commit
```

- 像squash一样合并,但是这个命令会放弃commit message(改动的文件内容没有变化)

```bash
f, fixup <commit> = like "squash", but discard this commit's log message
```


- 删除关于这条commit的所有文件改动(如果新增文件会被删除)

```bash
# x, exec <command> = run command (the rest of the line) using shell
```


- 删除关于这条commit的所有文件改动,并且删除该commit message(如果新增文件会被删除)

```bash
# d, drop <commit> = remove commit
```


## Miscellaneous

- 显示当前目录下所有文件(git bash)

```bash
ls -la
```

- 显示当前目录下所有文件(terminal)

```bash
ls
```

- 删除file_name

```bash
rm file_name
```

- 生成SSH Key

```bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```


- 在当前文件夹创建文件

```bash
echo >> file_name

echo off >> file_name
```



- 删除远程仓库内容

```bash
git remote remove origin
```

- 将所有工作区的改动临时保存在一个剪贴板中

```bash
git stash
```

- 将剪贴板的内容恢复到工作区

```bash
git stash pop
```

- 删除文件夹

```bash
rd file_name
```

- 以这个命名仓库名字，可以将仓库作为主服务器

**LSTUDIO2018.github.io**



## remote

- 为远程仓库取别名为origin(origin就代替了git@github.com:LSTUDIO2018/FuckThing.git) 

```bash
git remote add origin git@github.com:LSTUDIO2018/FuckThing.git
```

- 查看远程库信息

```bash
git remote 
```

- 查了与远程库链接信息

```bash
git remote -v
```

## Clone

- 从远端克隆下来不经过checkout(克隆下默认什么都不显示)
  - 使用git checkout [branch name] 在本地显示对应branch的内容

```bash
git clone --no-checkout [address] [new_repo_name]
```



 - 从远端克隆一个裸仓库(仅仅包含仓库信息) 

```bash
git clone --bare [address] [new_repo_name]
```




- 克隆上面那个裸仓库到本地

```bash
git clone [bare_address] [new_repo_name]
```



