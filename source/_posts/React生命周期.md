title: React生命周期
author: 葛亮均
tags: []
categories: []
date: 2019-08-15 17:50:00
---
学习水笔
``` bash
//组件被挂载之前
    componentWillMount(error, errorInfo) {
        console.log('componentWillMount')
    }
    
  //组件被挂载之后
    componentDidMount() {
        console.log('componentDidMount')
    }
    
  //组件被更新之前 //true返回需要更新
    shouldComponentUpdate(nextProps, nextState, nextContext) {
        console.log('shouldComponentUpdate')
        return true
    }
    
 //返回true需要更新时执行
    componentWillUpdate() {
        console.log('componentWillUpdate')
    }
    
  //组件更新完成之后
    componentDidUpdate(prevProps, prevState, snapshot) {
        console.log('componentDidUpdate')
    }
    
 //一个组件要从父组件接受函数
 //只要父组件的render函数被重新执行了。子组件的这个生命周期函数就会被执行
 //第一次存在父组件中不会执行，组件存在于父组件了才会执行
    componentWillReceiveProps(nextProps, nextContext) {
        console.log('componentWillReceiveProps')
    }
    
 //当组件被剔除时执行
    componentWillUnmount() {
        console.log('componentWillUnmount46546')
    }
 ```
