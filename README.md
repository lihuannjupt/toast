# toast1

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

# 代码中引用组件
import Toast from ./components/toast/Toast.vue';

# 文件中使用组件方法
```html
<template>
  <div>
    ...
    <Toast v-if='isToastShow' :time="time" :msg="message" :type="type" @function1="closeToast"></Toast>
    ...
  </div>
</template>

...
components: {
  Toast
}
...
```
# 组件使用
展示通过isToastShow进行,子组件提供function1方法，在消失后执行设定操作
# 组件参数
```javascript

     isToastShow: true,//toast展示与否，调用时设置，true为展示，false则不展示
      message: '不再提示了',//必填，展示的文字
      type: 'load',//展示的类型，可选normal,sus,err,load之一
      time:'5000'//展示的时间，单位ms
# 组件返回函数
function1(){
//toast在展示设定time后消失时触发的函数
}
