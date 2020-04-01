---
layout: post
title: "Git 回滚篇git revert"
description: ""
date: 2020-03-27
tags: [Git]
comments: true
share: true
---

**场景**：
1.项目上线，发现有bug，要紧急回滚到上个版本；
2.多人合作，在qa出现了蹊跷的bug，不确定是哪个分支带来的，下掉可疑分支；
3.产品觉得还是之前版本比较好。。

噔噔噔噔`git revert `闪亮登场！

1.回滚某次提交
`git revert commitId`

2.回滚多次提交
`git revert old-commitId^..new-commitId`

如果我们想把这三个revert不自动生成三个新的commit，而是用一个commit完成，可以这样：
`git revert -n old-commitId^..new-commitId`
如果回滚的提交并不连续，导致生成多个新的commit，可以这样：
`git rebase`合并多次commit:
`git rebase -i commitId` commitId是想要合并的起始commit，例如，先revert第三次提交，再revert第一次提交，想要只生成一条新的commit时,commitId为revert第三次提交的commitId。

3.回滚之后还想再恢复回来
如果在sim上回滚了feature/EDU-001分支，而后发现这个分支并没有问题，所以没有改动想要再合并到sim此时merge feature/EDU-001,会发现**没有任何可提交的更改**，*这是因为从时间的发生顺序来看，A分支第一次合并之前的修改发生在revert之前，revert发生在后，而 revert抛弃了A第一合并之前的修改，那么再合并Git就认为你永远抛弃了A第一次之前的修改。*
所以要解决这个问题，需要把revert产生的提交再revert一次。

参考链接：[https://blog.csdn.net/qq_35008279/article/details/86316819](https://blog.csdn.net/qq_35008279/article/details/86316819)

**为什么选择revert，不要reset？**
1.revert和reset相比有两个重要的优点。首先，它不会改变项目历史，对那些已经发布到共享仓库的提交来说这是一个安全的操作。
git reset 有很多种用法。它可以被用来移除提交快照，尽管它通常被用来撤销缓存区和工作目录的修改。不管是哪种情况，它应该只被用于本地修改。切记，你无权重设公共历史。

2.git revert 可以针对历史中任何一个提交，而 git reset 只能从当前提交向前回溯。
参考链接：[https://github.com/geeeeeeeeek/git-recipes/wiki/2.6-回滚错误的修改](https://github.com/geeeeeeeeek/git-recipes/wiki/2.6-%E5%9B%9E%E6%BB%9A%E9%94%99%E8%AF%AF%E7%9A%84%E4%BF%AE%E6%94%B9)
