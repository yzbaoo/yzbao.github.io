---
layout: post
title: "SourceTree 从下载、安装到免登录的方法（Windows 版 ）"
description: "工具"
date: 2018-04-20
tags: [工具]
comments: true
share: true
---

下载：链接: https://pan.baidu.com/s/1WNiSAP7EMANobIGC8xHYmw 密码: xxbt
1. 首先，安装完 SourceTree 以后先运行一次，弹出初始化登录页面后退出。
![图片描述][1]

2.找到 C:\Users\xx电脑名\AppData\Local\Atlassian\SourceTree文件下
增加名为accounts.json的文件
![图片描述][2]

accounts.json：

```
[  
    {  
      "$id": "1",  
      "$type": "SourceTree.Api.Host.Identity.Model.IdentityAccount, SourceTree.Api.Host.Identity",  
      "Authenticate": true,  
      "HostInstance": {  
        "$id": "2",  
        "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountInstance, SourceTree.Host.AtlassianAccount",  
        "Host": {  
          "$id": "3",  
          "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountHost, SourceTree.Host.AtlassianAccount",  
          "Id": "atlassian account"  
        },  
        "BaseUrl": "https://id.atlassian.com/"  
      },  
      "Credentials": {  
        "$id": "4",  
        "$type": "SourceTree.Model.BasicAuthCredentials, SourceTree.Api.Account",  
        "Username": "",  
        "Email": null  
      },  
      "IsDefault": false  
    }  
  ]  
```
重启软件

> 微信公众号：**前端实习日记**
  [1]: /images/20180425/1.png
  [2]: /images/20180425/2.png