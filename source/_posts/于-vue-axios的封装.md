title: 关于 vue axios的封装
author: 葛亮均
date: 2019-07-30 11:19:43
tags:
---
安装
``` bash
npm install axios -S
npm install --save axios vue-axios qs 
```
环境配置（楼主没有配置需要全局的可以引入）
``` bash
import axios from '../node_modules/axios'
Vue.prototype.$axios = axios;
```
新建 axios 文件夹下新建index.js
内容如下：
``` bash
import axios from 'axios'
import { Message } from 'element-ui'
const qs = require('qs')
if (process.env.NODE_ENV == 'production') { //正式环境
  axios.defaults.baseURL = 'http://192.168.1.254:8001/'
  /* axios.defaults.baseURL = window.location.protocol + "//" +  window.location.host; */
} else { //生产环境
  axios.defaults.baseURL = 'http://192.168.1.48:5000/api/p/'
}
/* axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded'; */ // 是否为from表单提交的传输对象 默认application/json
axios.defaults.headers.common['Accept'] = 'application/json, */*'
axios.interceptors.request.use(config => {
  let token = window.sessionStorage.getItem('token') // token的获取
  if (config.method === 'post' && config.headers['Content-Type'] != 'multipart/form-data') {
    /* config.data = qs.stringify(config.data); */ // 表单提交json转字符串
  }
  if (token) { // 统一header传送tonken
    config.headers.common['Access-Token'] = token
  }
  return config
}, error => {
  return Promise.reject(error)
})

axios.interceptors.response.use(response => { // 报错统一处理
  if (response.data.code === 500) {
    Message({
      message: response.data.message,
      type: 'warning'
    })
  }
  return response
}, error => {
  if (error.response.status == 401) { // 401 的处理
    sessionStorage.removeItem('token')
    return new Promise(() => {}) // pending的promise，中止promise链
  }
  return Promise.reject(error)
})
export default axios

```
按需引入
``` bash
import axios from '../../axios/index'
```

GET用法/POST用法
``` bash
 list () {
      let area = window.sessionStorage.getItem('area')
      axios.get('organization/list?area=' + area).then(res => {
        if (res.data.code === 200) {
          this.medicalList = res.data.data.list
        }
      })
    },
    //post
    axios.post('auth/login', params).then(res => {
            if (res.data.code == 200) {
              this.logining = false
              sessionStorage.setItem('token', res.data.data.access)
              let token = window.sessionStorage.getItem('token')
              if (token) {
                this.$router.push({path: '/home'})
              }
            } else {
              this.$message({
                type: 'error',
                message: res,
                center: true
              })
            }
          })
  ```