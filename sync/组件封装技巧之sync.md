## 组件封装技巧之sync

>prop为单向数据流，是不被建议在子组件里直接变更的

>.sync修饰符默认在根组件上注册监听事件(update:myPropName)，在子组件使用$emit方法触发监听事件改变绑定值,从而达到双向绑定

```html
  <div id="app">
    父组件中的title：{{title}}
    <text-document v-bind:title.sync="title"></text-document>
    <button @click="handleChange">parent</button>
  </div>
```
```js
Vue.component('text-document',{
      props:['title'],
      template:`
      <div>
        子组件中的title：{{title}}
        <button @click="handleChildrenChange">children</button>
      </div>
      `,
      methods:{
        handleChildrenChange(){
          this.$emit('update:title', "我被子组件改变")
        }
      }
    })
    new Vue({
      el:"#app",
      data:{
        title:""
      },
      methods:{
        handleChange(){
          this.title = "我被父组件改变"
        }
      }
    })
```

>注意带有 .sync 修饰符的 v-bind 不能和表达式一起使用 (例如 v-bind:title.sync=”doc.title + ‘!’” 是无效的)。取而代之的是，你只能提供你想要绑定的 property 名，类似 v-model。
