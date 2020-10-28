# vue入门学习
## 01 简介
### 特点
-  js框架
-  简化Dom操作
-  响应式数据驱动
## 02 vue程序

```
<div id="app">
        {{ message }}
</div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message:"   Hello Vue! "
            }
        })
    </script>
```
## 03 el 属性
- el 挂载点
  ```
  el命中的元素内部，使用两个大括号修饰的部分就会被data中同名的数据替换
  ```
- 作用
  - el是用来设置Vue实例挂载（管理）的元素
- 作用范围 会管理el选项命中的元素及其内部的后代元素
  - 元素内部
  - 元素外部不作用
- 选择器 可以使用其它的选择器，但是建议使用ID选择器
  - .class 类选择器
  - #id id选择器（建议）
  - div 标签选择器
- 设置其它dom元素 可以使用其它的双标签，不能使用html和body
  - 只能支持双标签（单标签内部无法写{{}}的内容）
  - vue无法挂载在html和body上
  - 建议挂载在div
## 04 data:数据对象
- data对象初始化
```
<script>
    var app = new Vue({
        el:"#app",
        data:{
            message:" Hello Vue! ",
            school:{
            name:"名字",
            mobile:"400"
        },
        campus:["1","2"]
        }
    })
</script>

```
- data调用内部元素
```
<div id="app">
    {{message}}   
    {{school.name}}
    {{school.mobile}}
    {{campus[1]}}
</div>
```
## 05应用
- 内容绑定 事件绑定
  - v-text
    - 设置标签的文本值（textContent）
        ```
        <h2 v-text="message+'!'"></h2>
        <h2>{{message+"!"}}深圳</h2>
        ```
        - 默认写法会替换全部内容，使用差值表达式{{}}可以替换指定内容
        - 内部支持写表达式
  - v-html
    - 设置标签的innerHTML
    - 其它与v-text类似
  - v-on基础  v-on等价于@
    - 作用:为元素绑定事件
    - 元素绑定
    ```
        <input type="button" value="事件绑定" v-on:事件名="方法">
        <input type="button" value="事件绑定" v-on:click="doIt">
        <input type="button" value="事件绑定" @click="doIt">
    ``` 
    - 事件方法  doIt是"方法"
    ```
    var app = new Vue({
        el:"#app",
        methods:{
            doIt:function(){

            }
        }
    })
    ```
    - 事件
      - click 点击事件
      - monseenter 鼠标移入事件
      - dblclick 双击事件
- 显示切换 属性绑定
  - v-show
  - v-if 
  - v-bind
- 列表循环 表单元素绑定
  - v-for
  - v-on补充
  - v-model
## 06 应用
- 创建Vue实例时，el 挂载点 data 数据 method 方法
- v-on指令的作用是绑定事件，简写用@
- 方法中通过this,关键字获取data中的数据
- v-text指令的作用是：设置元素的文本值，简写为{{}}
- v-html指令的作用是：设置元素的innerHTML
## 07 指令
### v-show
- v-show 根据表达式的真假，切换元素的显示和隐藏
- 原理是修改元素的display,实现实现隐藏
- 指令后面的内容，最终都会解析为布尔值
- 值为true元素显示，值为false元素隐藏
- 根据绑定的值进行判断
- 数据改变之后，对应的元素的显示状态会同步更新
```
<div id="app">
  <img src="地址" v-show="true">
  <img src="地址" v-show="isShow">
  <img src="地址" v-show="age>=18">
</div>
```
```
  var app=new Vue({
    el:"#app",
    data:{
      isShow=false,
      age:16
    }
  })
```
### v-if
- v-if 根据表达值得真假，切换元素得显示和隐藏（操作dom元素）
- 隐藏会直接将整个盒子remove后，显示会将整个盒子重新添加进去
```
<p v-if="true">我是一个p标签</p>
<p v-if="isShow">我是一个p标签</p>
```
```
var app=new Vue({
  el:"#app",
  data:{
    isShow:false
  }
})
```
- v-if指令的作用是：根据表达式的真假切换元素的显示状态
- 本质是通过操纵dom元素来切换显示状态
- 表达式的值为true，元素存在于dom树中，为false，从dom树中移除
- 值为true元素显示，值为false元素隐藏
### 区别
- 频繁操作的使用v-show操作，否则用v-if（v-if的开销会比较大）

### v-bind
- 设置元素的属性 src title class等写在元素内部的
- v-bind:属性名=表达式  v-bind可以省略
- v-bind指令的作用:为元素绑定属性
- 完整写法是v-bind:属性名
- 简写的话可以直接省略v-bind,只保留:属性名
- 需要动态的增删class建议使用对象的方式 
```
<img v-bind:src="imgSrc">
<img v-bind:title="imgTitle+'!!!!'">
<img v-bind:class="isActive?'active':''">
<img v-bind:class="{{active:isActive}}">
```
```
data:{
  imgSrc:"图片地址",
  imgTitle:"123",
  isActive:false
}
```
## 08 图片切换应用
- 列表数据使用数组保存
- v-bind指令可以设置元素属性，比如src
- v-show和v-if都可以切换元素的显示状态，频繁切换用v-show

### 09指令2
## v-for
- 据数据生成列表结构 响应式!!
- 数组经常和v-for结合使用
- 语法是(item,index) in 数据（数组）
- item和inde可以结合其他指令一起使用
- 数组长度的更新会同步到页面上，是响应式的
- html结构
```
<div id="app">
<ul>
  <li v-for="(item,index) in arr" :title="item">
    {{index}}{{item }}
  </li>
  <li v-for="(item,index) in objArr" :title="item">
    {{index}}{{item.name }}
  </li>
</ul>
</div>
```
```
var app = new Vue({
  el:"#app",
  data:{
    arr:[1,2,3,4,5],
    objArr:[
      {name:"jack"},
      {name:"rose"}
    ]
  }
})
```
## v-on补充
- 传递自定义参数，事件修饰符
- 事件绑定的方法写成函数调用的形式，可以传入自定义参数
- 定义方法时需要定义形参来接受传入的实参
- 事件的后面跟上.修饰符可以对事件进行限制（.push）
- .enter可以限制出发的按键为回车( @keyup.enter)
- [更多事件修饰符](https://cn.vuejs.org/v2/api/#v-on)
```
<div id="app">
  <input type="button" @click="doIt(p1,p2)"/>
  <input type="text" @keyup.enter="sayHi"/>
</div>
```

```
var app=new Vue({
  el:"#app",
  methods:{
    doIt:function(p1,p2){},
    sayHi:function(){}
  }
})
```
## v-model
- 获取和设置表单元素的值（双向数据绑定）(会自动进行数据的同步更新)
```
<input type="text" v-model="message" />
```
```
var app=new Vue({
  el:"#app",
  data:{
    messgae:"xzy"
  }
})
```
## 10 记事本应用
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class="app" id="app">
        <input v-model="inputdata" type="text" @keyup.enter="addli">
        <ul>
            <li v-for="(item,index) in list">
                    <p @click="removeli(index)">{{index}}{{item}}</p>
            </li>
        </ul>
        <span v-show="list.length!=0">总数:{{list.length }}</span>
        <input v-if="list.length!=0" type="button" @click="clear" value="清空全部">
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app=new Vue({
            el:"#app",
            data:{
                list:["写代码","吃饭饭","睡觉觉"],
                inputdata:"好好学习"
            },
            methods:{
                addli:function(){
                    this.list.push(this.inputdata)  
                },
                removeli:function(index){
                    this.list.splice(index,1);
                },
                clear:function(){
                    this.list=[]
                }
            }
        })
    </script>
</body>
</html>
```
## 11 网络应用 axios 网络请求库和Vue的结合
- 导包
```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```
- get请求
  - axios.get(地址?查询字符串).then(function(response){},function(err){})
- post
  - axios.post(地址,{key:value,key2:value2}).then(function(response){},function(err){})
- 接口事例
  - 接口1：随机笑话
  - 请求地址：https://autumnfish.cn/api/joke/list
  - 请求方法：get
  - 请求参数:num
  - 响应内容：随机笑话
  
  - 接口2：用户注册
  - 请求地址：https://autumnfish.cn/api/user/reg
  - 请求方法：post
  - 请求参数:username(用户名)
  - 响应内容：注册成功或失败
- git官网
  - https://github.com/axios/axios
