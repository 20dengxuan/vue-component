## 组件封装技巧之slot

> 目的：让插槽内容更够访问到子组件中的数据

```html
<div id="app">
  <template v-slot:cname="el">
    {{el}}
  </template>
</div>
```
```js
Vue.component('current-user',{
  data:function(){
    return {
      user: {
        lastName: 'd',
        firstName: 'x'
      }
    }
  },
  template:`
    <div>
      <slot name="cname" v-bind:user="user"></slot>
    </div>
  `
})
new Vue({
  el:"#app"
})
```