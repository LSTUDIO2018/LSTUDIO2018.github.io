---
title: Git Command
date: 2020-09-13 03:37:06


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



## repo


- 删除.git目录

```bash
rm -rf .git
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



## fast-forward

- 不使用fast-forward(快转机制)
  1. 要合并的[branch name]跟合并后的branch内容一样,会触发fast-forward
  2. 不使用fast-forward会保存所有提交

```bash
git merge [branch name] --no-ff
```




- 默认使用fast-forward
  1. master要合并develop分支，合并后与develop一致(内容一致)
  2. develop最新commit将不会显示在版本路线图中  

```bash
git merge [branch name]
```



## merge

- 恢复到合并前的状态

```bash
git reset --hard ORIG_HEAD
```




- 合并branch,但是先不提交commit(可以先测试合并是否成功),再考虑提交合并commit

```bash
git merge [branch name] --no-ff --no-commit
```




- 压缩[branch name]的commit(在合并后的branch里面不显示[branch name]的commit)

```bash
git merge --squash [branch name]
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




## Miscellaneous

- 显示当前目录下所有文件

```bash
git ls -la
```




- 在当前文件夹创建文件

```bash
echo >> <file>
```




- 删除远程仓库内容

```bash
git remote remove origin
```




- 以这个命名仓库名字，可以将仓库作为主服务器

**LSTUDIO2018.github.io**



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

