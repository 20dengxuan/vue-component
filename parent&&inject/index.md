## 组件封装技巧之parent And inject

> 目的：父组件方法提供给所有子组件使用

```html
  <div id="app">
    <user-name></user-name>
  </div>
```

```js
Vue.component('user-name',{
  inject:[getName],
  template:`
    <div>
      name:{{getName()}}
    </div>
  `
})
new Vue({
  el:"#app",
  parent: function(){
    return {
      getName: this.getName
    }
  },
  methods: {
    getName(){
      return "deng"
    }
  }
})

```