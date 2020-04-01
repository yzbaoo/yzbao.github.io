---
layout: post
title: "Git Submodules"
description: ""
date: 2020-04-01
tags: [Git]
comments: true
share: true
---

经常面临一些场景，想要把大代码库（repo）拆分成多个小的repo，例如：

现有代码库体积庞大，且模块管理混乱，经常容易错改别人的东西

某个模块需要单独构建，比如jQuery项目中的React试点、Node项目中的纯前端部分、Electron项目中的UI部分等等

某个模块是黑盒依赖项，开发中仅依赖其构建后的版本，比如框架类库等

针对诸如此类的情况，一般有3种解决方案：

1. npm package：把依赖项拆出去作为npm package，代码库随之独立出去
2. monorepo：单repo体积庞大没关系，分模块管理好就行
3. git submodules：把依赖项拆分到多个独立repo，作为主repo的submodule

##### **npm package**

npm package的优势在于成熟的管理依赖机制，规范且易用，缺点是主项目只能通过package版本号获取独立模块的更新，在主项目需要与子模块联调的场景就会非常麻烦：

*主项目：调不通啊
子模块：有点问题，我改一下...改版本号-构建-发布npm package
主项目：更新依赖，再试...还是调不通啊
子模块：还有点问题...*

频繁发版比较蠢，可以本地修改构建再拷贝一份过去，但还是有些麻烦。当然，通常可以通过mock接口或数据把联调依赖拆解开，但有时候mock全套API成本比较高，而且假的势必没有真的好用

##### **monorepo**
没有去了解

##### **git submodules**

git submodules提供了一种类似于npm package的依赖管理机制，包括添加、删除、更新依赖项等功能，区别在于前者所管理的依赖是子模块的源码，后者管理的是子模块的构建产物。在这一点上，git submodules与monorepo一致（都关心子模块的源码）

这样主项目需要与子模块频繁联调时的麻烦就不复存在了，因为主项目拉取到的submodules都是完整repo，可以直接修改-构建-提交

##### **git submodules vs npmpackage**

子项目与主项目联调比较方便，git submodules更适用于子项目与主项目是同一个团队开发。

建议浏览：[https://mobile.51cto.com/aprogram-393324.htm](https://mobile.51cto.com/aprogram-393324.htm)