# main.js入口文件



欸嘿嘿，首先我们先看下源码：

``` js
import Vue from 'vue'

import Cookies from 'js-cookie'

import 'normalize.css/normalize.css' // a modern alternative to CSS resets

import Element from 'element-ui'
import './styles/element-variables.scss'
import enLang from 'element-ui/lib/locale/lang/zh-CN'// 如果使用中文语言包请默认支持，无需额外引入，请删除该依赖

import '@/styles/index.scss' // global css

import App from './App'
import store from './store'
import router from './router'

import './icons' // icon
import './permission' // permission control
import './utils/error-log' // error log

import * as filters from './filters' // global filters


if (process.env.NODE_ENV === 'production') {
  const { mockXHR } = require('../mock')
  mockXHR()
}

Vue.use(Element, {
  size: Cookies.get('size') || 'medium', // set element-ui default size
  locale: enLang // 如果使用中文，无需设置，请删除
})

// register global utility filters
Object.keys(filters).forEach(key => {
  Vue.filter(key, filters[key])
})

Vue.config.productionTip = false

new Vue({
  el: '#app',
  router,
  store,
  render: h => h(App)
})

```



`main.js`入口文件很简单，没有什么复杂的逻辑；

就是将一些资源文件，样式文件以及`element-ui`组件，过滤指令等进行全局注册引用；

1. 引入`css`相关资源，`element-css, variables.css, global.css等`
2. 引入组件, `icon, element`
3. 自定义日志系统, 记录错误信息
4. `use-element`全局配置
5. `filter-hooks`等
6. `router, store`路由状态管理器等
7. 挂载元素

