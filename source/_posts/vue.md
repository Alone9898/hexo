title: vue自定义组件
author: 葛亮均
tags:
  - 技术
categories: []
date: 2019-07-01 18:39:00
---
``` bash
vue自定义公共组件

我们在编写页面的时候,会存在公共的组件,比如头部和底部菜单

我们拿公共头部为例子,想在每个页面都显示公共头部的实现方式有两种

在src/components目录创建目录 common, 再创建header.vue

header.vue的片段代码为
<template>
    <div>
        <h1>header in here</h1>
    </div>
</template>
<script>
    export default{}
</script>

(1)全局挂载组件
在main.js里挂载,通过Vue.component方式

import headerTop from "xxx/components/common/header"   //引入组件

Vue.component("head-view",headerTop);
 //第一个参数表示 head-view标签的内容都用第二个参数headerTop来代替

然后在需要使用的vue文件中引入头部的话,只需要加入 <head-view></head-view>标签


(2)局部引入,需要用的时候才引入使用
在需要使用的VUE文件中引入头部:
代码片段
<template>
<headerTopNav></headerTopNav>
</template>

<script>
 import headerTopNav from 'xxx/components/common/header'  //引入组件

export default{
components: {headerTopNav} //表示headerTopNav标签的内容被headerTopNav组件代替
}
</script>
--------------------- 
作者：Hobart-Ljw 
来源：CSDN 
原文：https://blog.csdn.net/baidu_32809053/article/details/80417783 
版权声明：本文为博主原创文章，转载请附上博文链接！

```
