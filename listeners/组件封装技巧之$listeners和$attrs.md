## 组件封装技巧之$listeners和$attrs

**目的**：使跟组件成为一个完全透明的包裹器，在根组件上使用子组件attribute和监听器

>**$listeners**: 包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 v-on="$listeners" 传入内部组件——在创建更高层次的组件时非常有用

>**$attrs**: 包含了父作用域中不作为 prop 被识别 (且获取) 的 attribute 绑定 (class 和 style 除外)。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 (class 和 style 除外)，并且可以通过 v-bind="$attrs" 传入内部组件——在创建高级别的组件时非常有用。

```html
  <div id="app">
   <base-input v-on:focus="onFocus"><base-input>
  </div>
```

```JS
  Vue.component('base-input',{
    inheritAttrs:false,
    porps:['label','value'],
    computed: {
      inputListeners: function() {
        var vm = this
        return Object.assign({},
        // 我们从父级添加所有的监听器
        this.$listeners,
        // 自定义监听器或覆写一些监听器的行为
        {
          // v-model
          input: function(event) {
            vm.$emit('input',event.target.value)
          }
        })
      }
    },
    template:`
      <label>
        {{label}}
        <input v-bind="$attrs" v-bind:value="value" v-on="inputListeners"
      </label>
    `
  })
  

  new Vue({
    el:"#app",
    data: {
      label:"我是label",
      value:"我是value"
    },
    methods:{
      onFocus(event){
        console.log(event)
      }
    }
  })
```

