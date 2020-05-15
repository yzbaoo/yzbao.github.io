---
layout: post
title: "code-splitting"
description: "由react-router引发的一堆之前没有深入了解的问题"
date: 2020-05-15
tags: [react]
comments: true
share: true
---


要知道按需加载分2种类型的文件

1. 按需加载组件
2. 按需加载redux模块

我们平时用的loadable只是按需加载其中的组件
#### **按需加载组件有4种方法：**

1. [bundle-loader](https://github.com/webpack-contrib/bundle-loader)
  代码搞得太长

  ![图片描述][1]

2. react-loadable
3. 在react-v16.6之后可以使用React.lazy和React.Suspense替换react-loadable
    
  ![图片描述][2]

  至于替换后的优点，目前只知道减少了2k大小的react-loadable库。。

4. 自定义lazyComponent

  ![图片描述][3]



#### **按需异步加载redux模块**
精髓：replaceReducer  
[Redux store 的动态注入](https://github.com/TongchengQiu/react-redux-dynamic-injection)

#### 使用dva时，如何动态注入store
  精髓：dynamic
  ![图片描述][4]

看下dynamic源码可以看到也是利用了replaceReducer改写reducer和saga。其思路跟[Redux store 的动态注入](https://github.com/TongchengQiu/react-redux-dynamic-injection)一样。

参考：

1. [React Router v4 之代码分割：从放弃到入门](https://segmentfault.com/a/1190000011426329)
2. [react按需加载](https://blog.csdn.net/weixin_36094484/article/details/80319385)
3. [在react-router4中进行代码拆分（基于webpack）](https://www.jianshu.com/p/547aa7b92d8c)
4. [使用 React.Suspense 替换 react-loadable](https://blog.csdn.net/roamingcode/article/details/85946380)
5. [从boilerplate中学到的redux里replaceReducer的按需使用](https://dreambo8563.github.io/2016/09/20/%E4%BB%8Eboilerplate%E4%B8%AD%E5%AD%A6%E5%88%B0%E7%9A%84redux%E9%87%8CreplaceReducer%E7%9A%84%E6%8C%89%E9%9C%80%E4%BD%BF%E7%94%A8/)
6. [Redux store 的动态注入](https://github.com/TongchengQiu/react-redux-dynamic-injection)
7. [dva-dynamic使用与实现](https://blog.csdn.net/yehuozhili/article/details/104058175)

[1]: /images/20200515/1.png
[2]: /images/20200515/2.png
[3]: /images/20200515/3.png
[4]: /images/20200515/4.png