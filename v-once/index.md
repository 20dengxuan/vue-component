## 组件封装技巧之v-once

> 目的： 通过v-once创建低开销的静态组件

- 渲染普通的 HTML 元素在 Vue 中是非常快速的，但有的时候你可能有一个组件，这个组件包含了大量静态内容。在这种情况下，你可以在根元素上添加 v-once attribute 以确保这些内容只计算一次然后缓存起来，

```js
 Vue.component("image-lists",{
   template:`
     <div v-once>
        <image src="#"></image>
        <image src="#"></image>
        <image src="#"></image>
        <image src="#"></image>
     </div>
   `
 })
```