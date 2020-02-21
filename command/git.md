## 创建库

```
echo "# unp1" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:libinyl/unp1.git
git push -u origin master
```


## remote

修改 origin:

```
git remote origin set-url [url]
```

## 回退单个文件

```
git checkout origin/master [filename]
```

## 冲突标记

```
本地
<<<<<< HEAD:file.txt
Hello world
=======
Goodbye
>>>>>> 77976da35a11db4580b80ae27e8d65caf5208086:file.txt
其他人
```

## 某文件的修改历史

```
git log filename
```

## 跟踪关系
```
// 查看跟踪关系
git branch -vv
// 设置跟踪关系
git branch --set-upstream-to=远端库名/远端分支名 本地分支名
```

## 重置

软重置到某一版本:
```
git reset hash值
```

## 分支
```
//查看所有分支
git branch -a 
//切换远程分支
git checkout -b 本地分支名 远程库/远程分支名
// 新建分支
git checkout -b xxx
git push origin newbranchname
// 删除本地分支
git branch -d localBranchName
// 删除远程分支
git push origin --delete remoteBranchName
```

## 对比远程与本地的差异
```
git fetch origin
git log master..origin/master
```


## diff

git diff HEAD 显示工作目录与git仓库之间的差异

## Git warning: push.default is unset; its implicit value is changing

## 报错处理

- The remote end hung up unexpectedly while git cloning

git config --global http.postBuffer 524288000

----

## 常用命令

 | 命令 | 描述
-|----|---
 | add | Add file contents to the index
 | bisect | Find by binary search the change that introduced a bug
 | branch | List, create, or delete branches
 | checkout | Checkout a branch or paths to the working tree
 | clone | Clone a repository into a new directory
 | commit | Record changes to the repository
 | diff | Show changes between commits, commit and working tree, etc
 | fetch | Download objects and refs from another repository
 | grep | Print lines matching a pattern
 | init | Create an empty git repository or reinitialize an existing one
 | log | Show commit logs
 | merge | Join two or more development histories together
 | mv | Move or rename a file, a directory, or a symlink
 | pull | Fetch from and merge with another repository or a local branch
 | push | Update remote refs along with associated objects
 | rebase | Forward-port local commits to the updated upstream head
 | reset | Reset current HEAD to the specified state
 | rm | Remove files from the working tree and from the index
 | show | Show various types of objects
 | status | Show the working tree status
 | tag | Create, list, delete or verify a tag object signed with GPG


## merge

## stash

git stash pop stash@{$num} 


bash 中:


function parse_git_branch {
    git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/' -e 's/((/(/' -e 's/))/)/'
}
function proml {
    local GREEN="\[\033[0;32m\]"
    local COLOR_END="\033[0m"
    PS1="[\u@\h:\W$GREEN\$(parse_git_branch)$COLOR_END]\$ "
}
proml

