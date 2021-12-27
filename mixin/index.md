## mixin

- 选项合并

> 当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”。
```js
var mixin = {
  data:{
    a: 1,
    b: 2
  },
  created(){
    console.log('hello from mixin')
  }
}
new Vue({
  data:{
    b:3,
    c:4
  },
  created(){
    console.log(this.$data)
    console.log('hello from component')
  }
})

// hello from mixin
// {a:1,b:3,c:4}
// hello from component

```

- 全局混入

> 全局混入，它将影响每一个之后创建的 Vue 实例
```js
Vue.mixin({
  created(){
    var myOption = this.$options.myOptions
    if(myOption){
      console.log(myOption)
    }
  }
})

new Vue({
  myOption:'hello'
})
```

- 自定义选项合并策略

> 自定义选项将使用默认策略，即简单地覆盖已有值。如果想让自定义选项以自定义逻辑合并，可以向 Vue.config.optionMergeStrategies 添加一个函数：
```js
Vue.config.optionMergeStrategies.myOption = (toVal, fromVal){
  // 返回合并后的值
}