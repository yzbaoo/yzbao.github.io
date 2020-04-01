---
layout: post
title: "Concurrent 模式"
description: ""
date: 2020-03-30
tags: [React]
comments: true
share: true
---

React 16.6 added a <Suspense>

**构造一个Concurrent UI：**

1.使用useTransition Hook 延迟切换页面；
2.使用suspense 确保切换页面后若还没有返回数据，显示loading。

总结：
体验不是很好，等待提示器时间是动态的可能会更好，如果数据很快返回却还要等3s的话，用户早走了，目前感觉作用不大。

注：***只有在React 的实验版本中才能采用Concurrent。***

`npm install react@experimental react-dom@experimental`

参考链接：https://zh-hans.reactjs.org/docs/concurrent-mode-reference.html