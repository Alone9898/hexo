title: vue判断滚动条到底部
author: 葛亮均
date: 2019-08-05 17:01:03
tags:
---

``` bashn
 mounted (){
       addEventListener('scroll', this.handleScroll)//监听函数
       }
       ```
``` bash
methods:{
  handleScroll() {
    //变量scrollTop是滚动条滚动时，距离顶部的距离
    let scrollTop = document.documentElement.scrollTop||document.body.scrollTop;
    //变量windowHeight是可视区的高度
    let windowHeight = document.documentElement.clientHeight || document.body.clientHeight;
    //变量scrollHeight是滚动条的总高度
    let scrollHeight = document.documentElement.scrollHeight||document.body.scrollHeight;
     //滚动条到底部的条件
     if(scrollTop+windowHeight == scrollHeight){
      //你想做的事情
     }
     }
     }
     ```