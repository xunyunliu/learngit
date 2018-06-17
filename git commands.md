## git local commands

| Command                      | Usage                                                        |
| ---------------------------- | ------------------------------------------------------------ |
| `git init`                   | create a git repo                                            |
| `git status`                 | check status of the repo                                     |
| `git diff filename`          | check file differences                                       |
| `git commit -m "add file"`   | make a new commit                                            |
| `git log [--pretty=oneline]` | display change log                                           |
| `git reset --hard HEAD^`     | Reset to the last commit                                     |
| `git reflog`                 | display the commands you have typed                          |
| `git checkout -- readme.txt` | reset the file to the state of the last `git commit` or `git add` |
| ` git reset HEAD <file> `    | You will need this to unstage file that has been added to index |
| `git rm test.txt`            | remove file from repository                                  |



## git remote commands

- When you have a empty remote repository and would like to associate it with your local repository, run the following command:

  ```bash
  git remote add origin git@github.com:michaelliao/learngit.git
  ```

- push the contents of the local repository to the remote repository.

  ```bash
   git push -u origin master
  ```

  由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送	的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。 

- 把本地`master`分支的最新修改推送至GitHub 

  ```bash
   git push origin master
  ```

- 要查看远程库的信息，用`git remote`：

  ```bash
  $ git remote -v
  origin  git@github.com:michaelliao/learngit.git (fetch)
  origin  git@github.com:michaelliao/learngit.git (push)
  ```

- 推送策略

  - `master`分支是主分支，因此要时刻与远程同步；
  - `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
  - bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
  - feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

- 创建远程`origin`的`dev`分支到本地  (`git clone`仅克隆master分支)

  ```bash
  git checkout -b branch-name origin/branch-name 
  git checkout -b dev origin/dev (example)
  ```

- 如果push命令由于冲突无法成功，首先运行`git pull`，在本地消除了conflict之后再push

  ```
  1. 首先，可以试图用git push origin <branch-name>推送自己的修改；
  
  2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
  
  3. 如果合并有冲突，则解决冲突，并在本地提交；
  
  4. 没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
  
  5. 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
  ```

- rebase操作可以把本地未push的分叉提交历史整理成直线 

  

## git branch commands

The relationship between HEAD and master

![0](../../../Downloads/0.png)

- create a new branch

```bash
git checkout -b feature1
```

- merge a branch

```bash
git merge feature1
```

- merge a branch without fast forward (this is going to create a new commit)

```bash
git merge --no-ff -m "merge with no-ff" dev
```

- delete a branch

```bash
git branch -d feature1
```

- check the status of merging

```bash
git log
```

- handle merge conflict

  update the file that causes the conflict

- preserve the current working state

  save:

  ```bash
  git stash
  ```

  load:

  ```bash
  git stash pop or git stash apply stash@{0}
  ```

  check state:

  ```bash
  git stash list
  ```

  