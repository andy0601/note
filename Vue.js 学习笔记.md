# Vue.js 学习笔记

## Vue CLI相关笔记
### @vue/cli 3.x
#### 安装
```powershell
npm install -g @vue/cli
```

#### 初始化项目
```powershell
vue create project-name
```

#### 现有项目中安装插件（如ESLint, vue-router, vuex）等
```powershell
vue add @vue/eslint
vue add router
vue add vuex
```

#### package.json里的ESLint配置
```json
{
  "eslintConfig": {
    "root": true,
    "env": {
      "node": true
    },
    "extends": [
      "plugin:vue/essential",
      "@vue/standard"
    ],
    "rules": {
      "generator-star-spacing": "off",
      "no-debugger": "off",
      "no-console": "off",
      "indent": 0
    },
    "parserOptions": {
      "parser": "babel-eslint"
    }
  }
}
```

## Vue.js Fundamentals
### 第二课：入门

**`javascript`**

```javascript
var app = new Vue({
    el: '#app',
    data: {
        message: 'Hello world!'
    }
})
```
**`HTML`**

```html
<div id="app">
    <h1>{{message}}</h1>
</div>
```

在控制台输入 `app.message = '你好'` 则可以改变HTML中的文字

### 第三课

**v-text v-html**

**`javascript`**

```javascript
var app = new Vue({
    el: '#app',
    data: {
        message: 'Hello world!'
    }
})
```
**`HTML`**

```html
<div id="app">
    <h1 v-text="message"></h1>
</div>
```

**v-show** 布尔型，控制元素是否显示

**v-if v-else** 判断条件

**v-pre** 直接输出花括号内容，没有值

**v-once** 直接渲染无法更改

**v-cloak** 程序执行之后再渲染到页面

### 第四课 **v-bind** 数据绑定

**`javascript`**

```javascript
var app = new Vue({
    el: '#app',
    data: {
      message: 'Hello world!',
      title: 'Boo ya!',
      url: 'https://cn.vuejs.org/images/logo.png'
    }
  })
```
**`HTML`**

```html
<div id="app">
    <h1 v-bind:title="title">{{message}}</h1>
    <img :src="url" alt="">
</div>
```

### 第五课 **v-for** 循环
```javascript
var app = new Vue({
    el: '#app',
    data: {
      message: 'Hello world!',
      todos: [
        { text: 'Learn Vue'},
        { text: 'Like the video'},
        { text: 'Subscribe to DevMarketer'}
      ]
    }
  })
```
**`HTML`**

```html
<div id="app">
    <h1>{{message}}</h1>
    <ul>
        <li v-for="todo in todos">{{ todo.text }}</li>
    </ul>
</div>
```

### 第六课 **`v-model`**
实时双向绑定

```javascript
var app = new Vue({
    el: '#app',
    data: {
      message: 'Hello world!'
    }
  })
```
**`HTML`**

```html
<input type="text" v-model="message">
```

### 第七课 事件处理
**`v-on:click`**
**`@click`**
**`methods`**

### 第八课 **`computed`**

### 第九课 Getter & Setter
 
## 其它课程笔记
### 列表删除某一项元素
```vuejs
new Vue({
  el: '#app',
  method: {
    remove(todo) {
      this.todos = this.todos.filter(item => item !== todo)
    }
  }
})
```

### 自定义指令
```vue
<template>
  <div id="app">
    <div v-color="flag">变色</div>
    <div v-drag>拖我</div>
  </div>
</template>

<script>
let app = new Vue({
  directives: {
    color(el, bindings) {
      el.style.background = bindings.value
    },
    drag(el) {
      el.onmousedown = function(e) {
        let disx = e.pageX - el.offsetLeft
        let disx = e.pageY - el.offsetTop
        
        document.onmousemove = function(e) {
          el.style.left = e.pageX - disx + 'px'
          el.style.top = e.pageY - disy + 'px'
        }
        
        document.onmouseup = function() {
          document.onmousemove = document.onmouseup = null
        }
        
        e.preventDefault()
      }
    }
  },
  data: {
    flag: 'red'
  }
})
</script>

<style scoped>
  .flag {
    position: absolute;
    width: 100px;
    height: 100px;
    color: lightseagreen;
  }
</style>
```

