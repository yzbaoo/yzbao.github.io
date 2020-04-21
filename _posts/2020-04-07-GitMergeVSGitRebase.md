---
layout: post
title: "git merge和git rebase的区别"
description: "rebase目前很少用，以后要增加使用"
date: 2020-04-07
tags: [Git]
comments: true
share: true
---

rebase 跟 merge 的区别你们可以理解成有两个书架，你需要把两个书架的书整理到一起去，第一种做法是 merge ，比较粗鲁暴力，就直接腾出一块地方把另一个书架的书全部放进去，虽然暴力，但是这种做法你可以知道哪些书是来自另一个书架的；第二种做法就是rebase ，他会把两个书架的书先进行比较，按照<u>**购书的时间来**</u>给他重新排序，然后重新放置好，这样做的好处就是合并之后的书架看起来很有逻辑，但是你很难清晰的知道哪些书来自哪个书架的。

只能说各有好处的，不同的团队根据不同的需要以及不同的习惯来选择就好。

rebase本质上是线性的cherry-pick。

rebase 和 merge 的另一个区别是rebase 的冲突是一个一个解决，如果有十个冲突，先解决第一个，然后用命令

`git add -u`
`git rebase --continue`

继续后才会出现第二个冲突，直到所有冲突解决完，而merge 是所有的冲突都会显示出来。

另外如果rebase过程中，你想中途退出，恢复 rebase 前的代码则可以用命令

`git rebase --abort`

**参考链接：**

1. [gitbook中文版-rebase](http://gitbook.liuhui998.com/4_2.html)
2. [聊一下git rebase -i](https://www.cnblogs.com/wangiqngpei557/p/5989292.html)
3. [合并多个commit](https://www.jianshu.com/p/964de879904a)