---
layout: post
title: "前端数据可视化之 --- （一）亿级关系图"
description: ""
date: 2018-05-16
tags: [cytoscape]
comments: true
share: true
---


**前言**
--
在这之前，提起数据可视化，我都是能用echarts尽量用echarts，特效很棒而且用起来简单，粘贴一个option改个data就能生成很酷炫的报表，但是真正走向数据可视化领域之后，还是会发现echarts有些不足，而且做大数据分析的企业全都依靠使用echarts的话，那么你们的系统在表现上就已经输了。
现在来看的话，大数据分析是互联网发展必然的产物，所以掌握数据可视化工具的前端工程师在未来会是最基本的要求，然而在那个时候你还仅仅会使用某chart，那么你自身的竞争力在哪。
最终实现效果：https://yzbaoo.github.io/cytoscape/

**cytoscape**
---------

看了上面的需求你会选择用什么库实现? echarts应该是实现不了了(也可能是我对echarts的属性研究不深)，D3？(D3是肯定可以的了)，与其用D3从零开始为什么不找到现有的开源的专门做关系图的库，来实现它，百度了半天也没搜出个一支半截，最终还是看了某查网，发现它们引入了一个叫cytoscape.js的文件，百度了一下（官网：http://js.cytoscape.org/）

**描述**

> Cytoscape.js is a fully featured graph theory library. Do you need to
> model and/or visualise relational data, like biological data or social
> networks? If so, Cytoscape.js is just what you need.
> 
> Cytoscape.js contains a graph theory model and an optional renderer to
> display interactive graphs. This library was designed to make it as
> easy as possible for programmers and scientists to use graph theory in
> their apps, whether it's for server-side analysis in a Node.js app or
> for a rich user interface.

这是文档给出的描述，说的很官方，大概意思就是如果你想要“关系”关系图的话你可以使用它，包括分子图、社交网络图一系列想要表达关系的图，并且提供可以用JS原生方法添加交互的API。ok你的关系图做的很牛逼就够了，这正是我们想要的。使用方法很简单，一个div用于盛装画好的图，先引[jquery][1]，再引[Cytoscape.js][2]，然后就可以开始写你的代码了，还支持使用npm安装。

**demo**
----
代码：https://github.com/yzbaoo/cytoscape
上来，调用cytoscape方法，参数主要包括：

```
var cy = cytoscape({
    container: document.getElementById('cy'),
    style:[
        {
            selector:'node',//点的样式，同理还有边的"edge",也可以新增一个类名，然后在事件里面add和remove来改变点和边的样式
            style:{}
        }
    ],
    elements:{//图数据
        node:[],
        edges:[]
    },
    layout:{//包含一些设置图布局的属性
        name: 'breadthfirst',//用哪种方式排列，可选：breadthfirst(广度优先)、cose(缝制，乱交)、preset(预设)、circle(圆形)、grid(矩形)
        animate:true,//出来动画
        ...
    }
})
//添加交互事件
//点：
cy.on("mouseover", "node", function (a) {
    $('#cy').css('cursor', 'move');
    let c = a.target;
    c.addClass("nodeHover");
    cy.collection("edge").removeClass("edgeActive");
    c.neighborhood("edge").addClass("edgeActive");//鼠标经过某节点，与此节点有关的变高亮显示
    //c.neighborhood("edge")表示：跟当前节点有关系的边
})
cy.on("mouseout", "node", function (a) {})
cy.on("click", "node", function (a) {})
cy.on("vmousedown", "node", function (a) { //监听鼠标左键按下})
cy.on("tapend", "node", function (a) { //监听鼠标左键释放})
//线：
//同理线的事件将‘node’换成‘edge’就行了
```

这里个人感觉，有了.neighborhood("node/edge")方法，就可以吃遍天了，基本的需求要么就是target自身添加一些样式，要么就是neighborhood（邻居）添加一些样式了，除了target就是neighborhood了嘛，他俩就已经可以表示全部。

**问题**
--
在react项目中使用，虽然官方支持npm安装，也有react cytoscape包，但是使用方法还是很鸡肋，如下：

```
render(){
    return(
        <ReactCytoscape 
        containerID='cy'
        elements={this.getElements()}
        style={this.cyStyle()}
        cyRef={(cy) => {this.cyRef(cy)}}
        cytoscapeOptions={{maxZoom:2.5}}
        layout={layout}
        />
    )
}
...
//鸡肋在此
cyRef = (cy) => {
    cy.on("mouseover","node",function(a){
        $('#cy').css('curser','move');
        let c = a.target;
        cy.collection("edge").removeClass("edgeActive");
        c.neighborhood("edge").addClass("edgeActive");
    })
    
}
```
在cyRef 方法中，还是要像原生一样操作实际DOM，这似乎有些不符合react的代码规范和设计理念。因为目前国内使用cytoscape的很少，论坛上也没有多少资源，期待大家在使用之后能回到此处在做交流，我遇到的这些问题你是否也遇到了，如何解决的我们可以做一些探讨。

**交流**
--

**此外**，你们在做数据可视化的时候使用的是什么库，都是D3吗？还是svg去画，还是公司内有非开源的图表库？欢迎加入***前端可视化技术群*** 群二维码7天内有效,由下进入segmentfault有二维码。



  [1]: http://www.bootcdn.cn/jquery/
  [2]: http://www.bootcdn.cn/cytoscape/