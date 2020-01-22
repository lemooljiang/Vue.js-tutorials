# <center>Vue基础</center>

## 目录
- [vue实例的生命周期](#vue实例的生命周期)
- [基础使用](#基础使用)
- [常用表达式](#常用表达式)
- [class样式](#class样式)
- [事件修饰符](#事件修饰符)
- [按键修饰符](#按键修饰符)


## vue实例的生命周期
![vue实例的生命周期图](./images/vue-lifecycle.png)
+ 什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！
+ 生命周期钩子：就是生命周期事件的别名而已；
+ 生命周期钩子 = 生命周期函数 = 生命周期事件
+ 主要的生命周期函数分类：
 - 创建期间的生命周期函数：
  	+ beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
  	+ created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板
  	+ beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中
  	+ mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示
 - 运行期间的生命周期函数：
 	+ beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染dom节点
 	+ updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！
 - 销毁期间的生命周期函数：
 	+ beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。
 	+ destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

```js
beforeCreate(){
    console.log('实例刚刚被创建1');
},
created(){
    console.log('实例已经创建完成2');
},
beforeMount(){
    console.log('模板编译之前3');
},
mounted(){     /*请求数据，操作dom , 放在这个里面  mounted*/
    console.log('模板编译完成4');
},
beforeUpdate(){
    console.log('数据更新之前');
},
updated(){
    console.log('数据更新完毕');
},
beforeDestroy(){   /*页面销毁的时候要保存一些数据，就可以监听这个销毁的生命周期函数*/
    console.log('实例销毁之前');
},
destroyed(){
    console.log('实例销毁完成');
}

//页面一创建就执行的方法
为了使一些函数自动执行，可以把它们挂载在这些钩子函数上。
mounted(){
      this.setMessage();
    },

```

## 基础使用
```html
//Vue.js v2.6.6
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo</title>
    <script src="./src/js/vue.js"></script>
</head>
<body>
    <div id="app"><p>{{ msg }}</p></div>   //view层
<script>
    var app = new Vue({  //VM调度者
        el: '#app',
        data: {
            msg: 'hello world'   //Model层
        }
    })
</script>
</body>
</html>
```

## 常用表达式
```html
1、v-cloak 解决插值表达式的闪烁问题，后面不再需要
  <p v-cloak>{{ msg }}</p>  
  [v-cloak]{
    display: none;
  }

2、<p v-text='msg'></p>  // 渲染文本内容，会替换整个文本，所以一般使用插值表达式{{ msg }}

3、<p v-html="msg2"></p>  // 渲染html内容
   msg2: '<h1>title 1</h1>'  

4、v-bind:title='mytitle'     /绑定变量属性
   语法简写形式：v-bind:title -> :title='mytitle'

5、v-on:click='show'  /绑定事件
    需要定义methods
    methods:{
    show: function () {
    alert('hello world')
    }
    }
语法简写：v-on:click -> @click
其它： v-on:mouseover 

6. v-model,双向数据绑定(与表单结合,input,select,checkbox,textarea,form)：
  <input type="text" v-model="msg">
  msg: hello world,

7. v-for：
遍历数组：
  <p v-for='item in list'>{{item}}</p>
遍历对象：
  <p v-for= '(val, key) in user'>{{val}}—{{key}}</p>
遍历数字：
  <p v-for="count in 10">{{ count }}</p>

8. v-if ,v-show：
<p v-if='true'>显示出来</p>  //v-if每次会重新生成和删除元素
<p v-show='true'>显示出来</p> //v-show只是隐藏显示
```

## class样式
```html
1. 数组
  <h1 :class="['first', 'second']">hello</h1>
2. 三元表达式  
  <h1 :class="['first', 'second',flag?'active':'']">
3. 类名
  <h1 :class="['first', 'second', { 'active':flag }]">
4. 直接使用类
 <h1 :class="{first:true, second:true}"}>hello</h1>
```


## 事件修饰符
```js
.stop @click.stop='show'   //可以阻止事件冒泡
.prevent  //阻止默认行为
.capture  //捕获触发事件
.self     //只有点击当前元素才触发
.once    //只触发一次
```

## 按键修饰符
```js
@keyup.enter='function'
.enter  //监听enter键
.tab
```