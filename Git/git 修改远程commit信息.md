---
title:  git 修改远程commit信息
tags: git,commit,remote
grammar_cjkRuby: true
---


---
### 修改==git commit==信息
　　在一次提交中，有可能会把一些错误的信息提交到==git==中，并且已经==push==到了远程仓库上，例如：不小心把系统的时间进行了调整，调整到了很久以前或者很早以后，自己当时并不知道，并且提交并==push==到了远程仓库中，这时候==commit==会在很后面或者一直在前面，很显眼，怎么补救？
　　1.找到==commit==号 像这样`27d37ce`
　　2.使用命令 `git  rebase --interactive 27d37ce^` 这样会回到当前==commit==号的编辑模式
　　3.找到要修改的==commit== 把前面的`pick`修改成`edit` 
　　4.这时候会提示两个命令，`git commit --amend`与`git rebase --continue`，其中`git commit --amend`表示去修改`edit`的==commit==的内容，`git rebase --continue` 表示回复到顶端==commit==指针
　　5.使用`git commit --amend`命令，这们就可以修改==commit==中的信息了
　　6.然后使用`git rebase  --continue`完成==rebase==操作，回到指向最前的==head==
　　7.最后使用`git push -f`强制==push==到远程分支，注意使用`git push -f`时要保证本地分支与远程在修改前是一致的，否则不一致的地方会被强制==push==覆盖掉
　　8.现在已经把==push==到远程仓库的==commit==的信息修改掉了
  　　