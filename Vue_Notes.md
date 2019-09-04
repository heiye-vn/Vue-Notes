# Vue Study Notes


## 1.基本指令

- **v-text**：插入文本

  ```html
  <p> {{变量名}} </p>			<!-- 注：vue中data函数返回一个对象（变量名:值） -->
  <p v-text="变量名"></p>		<!-- 通过ES5字符串添加 -->
  <p v-text=`${变量名}`></p>		<!-- 通过ES6模板字符串添加（注：变量需要使用${}） -->
  <p v-text=`${变量名}`>2333</p>	<!-- 在标签内添加内容会被v-text覆盖 -->
  ```

- **v-html**：渲染html标签（dom元素）

  ```html
  <h2 v-html="变量名"></h2>		<!-- 获取后端传来的dom元素进行渲染 -->
  ```

- **v-show**：根据表达式的真假值来渲染dom元素，动态切换dom元素的 display 属性值（接收一个bool值，传入其他值能够进行隐式转换）（元素的隐藏与显示）

  ```html
  <p v-show="变量名">Hello World</p>		<!-- 当v-show中变量的值为假时p元素添加一个display:none属性，为真时display为默认值 -->
  ```

  

  **扩展**：vue是能够响应式的改变视图的（dom元素内容），底层存在一个虚拟dom和 diff 算法进行响应式改变数据

  

- **v-if**：根据表达式值的真假来渲染dom元素，通过 createElement 和 removeElement 方法来创建/移除dom元素（接收一个bool值，其他值能够进行隐式转换）（元素的存在与消失）

  ```html
  <p v-if="变量名">Hello Vue</p>			<!-- 值为真时 create 一个dom元素，为假时 remove 该dom元素 -->
  
  <div v-if="type === 'a'"> 这是A用户 </div>  		<!-- 使用v-if判断表达式的值来进行不用的渲染 -->
  <div v-else-if="type === 'b'"> 这是B用户 </div>
  <div v-else> 这是{{type.toLocaleUpperCase()}}用户 </div>	<!-- v-else-if前面搭配v-else-if或者v-if，v-else前面搭配v-else-if或者v-if。总之，使用后面两个必须要和v-if一起使用 -->
  ```

  

  **注**：当 v-for 和 v-if 一起使用时，v-for 的优先级要比 v-if 高（后面详解）

  

- **v-on**：绑定事件监听器

  ​	  v-on:事件类型='函数名'，简写（@:事件类型='函数名'）

  ```html
  <!-- 不同的语法 -->
  <button @click='onAdd'>增加</button>
  <button v-on:click='onReduce'>减小</button>
  <input @keyup="onEnter" placeholder="允许触发所有的键盘事件">
  <input @keyup.13="onEnter" placeholder="设置enter键值添加enter键盘事件">
  <input @key.enter(space...)='函数名' placeholder='通过设置单独的键名来绑定事件'>
  <button @click.once="once">点击一次</button>    <!-- 设置.once来限制仅点击一次，（两次，三次等无效） -->
   <button v-on='{mousedown:onAdd,keyup:onReduce}'>对象语法</button>		<!-- 通过对象语法来监听不同的事件从而执行不同的函数 -->
   <button v-on="{mousedown,keydown}">对象语法扩展</button>		<!-- 扩展：对象的键值对相同（key，value） -->
  
  <!-- form表单提交默认会跳转，通过 .prevent阻止跳转、.stop阻止事件冒泡 -->
  <form method="GET" action="https://www.baidu.com/" @submit.stop.prevent="Submit">
  	<input type="submit">
  </form>
  ```

  

- **v-bind**：**动态**地绑定一个或多个特性，或一个组件 prop 到表达式

  ```html
  <!-- 不同的语法 -->
  <img v-bind:src="变量名" width="100" alt="">
  <img :src="变量名" width="100" alt="">				<!-- 简写 -->
  <!-- 绑定自定义属性 -->
  <p :name='Attr'></p>

  <!-- 内联字符串拼接 -->
  <img :src="'img/'+localImg" width="400" alt="">
  <img :src="`img/${localImg}`" width="400" alt="">
  
  <!-- id,class绑定 -->
  <p :class='box'></p>
  <p :id='wrap'></p>
  
  <!-- 对象语法绑定属性 -->
  <h2 :class='{blue:isBlue}'>对象语法绑定属性，属性的值为布尔值</h2>
  <h2 :class='{red,blue}'>对象语法绑定属性，属性的值为布尔值</h2>
  <!-- {red,blue} <==> {red:red,blue:blue} -->
  
  <!-- 数组方法绑定属性 -->
  <h2 :class='["lime"]'>数组方法绑定属性</h2>
  <h2 :class='[isYellow,isGreen,{classB:isB,classC:isC}]'>数组方法绑定属性,isB,isC是布尔值</h2>
  
  <!-- style 绑定 -->
  <h2 :style="{color:'blue',border:border}">对象方法绑定内联样式</h2>
  <h2 :style="styleObj">对象方法绑定内联样式</h2>
  ```
  
  
  
- **v-for**：基于列表渲染

  ```html
  <!-- 不同的语法 -->
  <!-- 渲染数组 -->
  <ul>
      <!-- <li v-for='item in arr' :key='time'>{{item}}</li> -->
      <li v-for='(item,index) in arr' :key="index">{{item}}</li>
  </ul>
  
  <!-- 渲染对象 -->
  <ol>
      <!-- <li v-for='(item,index) in userInfo'>{{item}} 值</li> -->
      <li v-for='(item,key,value,index,a) in userInfo'>
          item:{{item}}<br>
          key:{{key}}<br>
          value:{{value}}<br>
          index:{{index}}<br>
          a:{{a}}
      </li>
  </ol>
  
  <!-- 渲染请求到的数据 -->
  <ol>
      <li v-for=' item in todos' :key='item.id'>{{item.title}}</li>
  </ol>
  ```

  

  **注：**使用 v-for 指令来渲染一个列表，使用 item in items 的形式来渲染，其中 items 是要渲染的数据，item 是被迭代的每一项数据的别名（可以包含很多项，index、id、value等）；可以使用 of 代替 in 作为分隔符；

  建议尽可能在使用 `v-for` 时提供 `key`（类型：**number**、**string**） attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升，key是vue识别节点的一个通用机制

  

- **V-model**：在表单控件或者组件上创建双向绑定（随着表单控件类型不同而不同）

  ​	原理：底层通过虚拟dom和diff算法，响应式的对用户更新的数据进行渲染

  ```html
  <!-- 语法 -->
  <div id='app'>
  	<h1>
      	{{msg}}
  	</h1>
      <input type='text' v-model='msg' />
  </div>
  
  <!-- 响应式的更新用户输入的数据 -->
  
  ```

  

## 2.全局API

- **Vue.extend( options )：**使用基础 Vue 构造器，创建一个“子类”。参数是一个包含**组件**选项的对象

  **注：**`data` 选项是特例，需要注意 - 在 `Vue.extend()` 中它必须是函数

  ```html
  <div id='app'>
      <abc></abc>
  </div>
  ```

  ```javascript
  // 创建构造器
  const extend =  Vue.extend({
      template:`<h1><a :href='url'>{{con}}</a></h1>`,
      data(){                  // 注，在Vue.extend中data类型必须为一个函数
          return {
              url:'http://wwww.baidu.com',
              con:'跳转至百度'
          }   
      }
  });
         
  // 创建一个extend实例，并挂载到一个元素上
  new extend().$mount('abc'); 
  // console.log(new extend())
  ```

  

- **Vue.nextTick([ callback,context ])**

  ​	在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM

```html
<div id='app'>
    <h1>
        {{title}}
    </h1>
</div>
```

```javascript
const app = new Vue({
    el:'#app',
    data(){
        return {
            title:'Hello WOrld'
        }
    }
});
app.title = 'Hello Vue'      // 修改了数据，但是DOM还没更新

// 因为nextTick延时，故在视图渲染结束之后通过该方法操作dom
Vue.nextTick(()=>{
    // 此时DOM已经更新完成且可以继续操作dom节点
})
// 由于Vue2.1.0返回了一个Promise（不存在回调且支持Promise的环境）
Vue.nextTick().then(()=>{
    // 可以继续操作dom节点
})
```



- **Vue.set( target,propertyName/index,value )**

  向**响应式对象**中添加一个属性，且确保该新属性也是响应式的，并触发视图更新

  **注**：对象不能是Vue实例，或者Vue实例的根数据对象

  ```html
  <!-- 语法 -->
  <div id='app'>
      <!-- 内部调用方法 -->
      <ul>
          <li v-for='item in arr'>{{item}}</li>
      </ul>
      <input text='button' @click='changeClick' value="点击改变">
  </div>
  	<!-- 外部调用方法 -->
  	<input text='button' onclick='handleClick' value="点击改变1">
  ```

  ```JavaScript
  const vm = new Vue({
      el:'#app',
      data(){
          return {
              arr:['小红',"菲菲","小明"]
          }
      }，
      methods:{
      	changeClick(){
      		this.$set(this.arr,0,"小虎")		// 点击时 小红->小虎
  		}
  	}
  });
  // 在#app外部调用Vue.set方法
  function handleClick(){
      //vm.$set(vm.arr,0,"小虎")		//使用实例对象调用set方法（要添加$符号）
      Vue.set(vm.arr,0,"小虎")			// 使用构造函数调用set方法（需用添加$符号）
  }
  ```

  

  **扩展：**vue核心工作原理

  ```javascript
  var obj ={};
  	Object.defineProperty(obj,'param'{
      	set:function(newVal){
          	console.log('添加了一个属性')
          	this._param = newVal
      	},
          get:function(){
              console.log('获取值')
              return this._param
          }
      })
      // 会通过底层监听执行set方法
      obj.parma = 'newparma'  	// "添加了一个属性"  "newparma"
  	
  	//自动执行get方法（响应式处理）
  	console.log( obj.parma )	// "获取值"  newparma
  ```

  

- **Vue.delete( target,propertyName/index )**

  删除对象的属性。如果对象是**响应式**的，确保删除能触发更新视图。这个方法主要用于避开 Vue 不能检测到属性被删除的限制，但是你应该很少会使用它

  语法类似（Vue.set）

  

- **Vue.directive( id,[ difinition ] )**

  注册或者获取全局指令

  **注：**先注册指令，再在实例化对象中使用

  ```html
  <div id='app'>
      <p v-zsp='custom'></p>
  </div>
  ```

  ```javascript
  // 注册全局指令
  Vue.directive('zsp',(el,bind)=>{
      //console.log(el,bind)
      el.innerText = bind.value
      el.style="......"
  });
  // 在实例化对象中使用指令
  const vm = new Vue({
      el:"#app",
      data(){
          return{
              custom:'这是封装的一个自定义全局指令'
          }
      }
  })
  ```

  

- **Vue.filter( id,[difinition] )**

  ​	注册或获取全局过滤器

  ```html
  <div id="app">
  	<h1>{{ msg | myFilter }}</h1>
  	<ul>
     		<li v-for='item in info' :key='item.id'>{{item.name}}</li>
  	</ul>
      <input type="button" @click='changeClick' value='点击 过滤'>
  </div>
  ```

  ```JavaScript
   const vm = new Vue({
              el: '#app',
              // 注册过滤器（自动过滤）
              filters:{
                  myFilter(value){
                      return value.split('').reverse().join('')
                  }
              },
              data() {
                  return {
                      msg: 'Vue.filter()',
                      info:[
                          {id:1,name:'书包'},
                          {id:2,name:'铅笔'},
                          {id:3,name:'本子'}
                      ]
                  }
              },
       		// 添加函数方法，手动过滤	
              methods:{
                  // 通过点击 调用函数中的过滤方法
                  changeClick(){
                      this.info = this.info.filter(item=>item.id !== 3)
                  }
              }
          });
  ```

  

- **Vue.component( id,[ difinition ] )**

  ​	注册或者获取全局组件，注册还会自动使用给定的 id 设置组件名称

```html
<div id='app'>
    <!-- 组件渲染标签用 - 隔开，且字母全部小写 -->
    
    <v-header-nav></v-header-nav>		<!-- 全局组件 -->
    <my-component></my-component>
    
    <top-nav></top-nav>					<!-- 局部组件 -->
    <left-nav></left-nav>
</div>
```

```JavaScript
//注册全局组件
Vue.compoment('vHeaderNav',{
    template:`<p>这是vHeaderNav组件</p>`
});
Vue.component(
	"myComponent",			// 组件名建议使用驼峰命名
    Vue.extend(
    	template:`<h1><a :href="url">{{con}}</a></h1>`,
        data(){
    	   return{
    			url:'http://www.baidu.com',
    			con:'跳转至百度'
 		}})
)

const app = new Vue({
    el:"#app",
    components;{		// 注册局部组件
    	topNva:{template:`<p style="color:red">这是topNav组件</p>`},
        leftNva:{template:`<p style="color:blue">这是leftNav组件</p>`}
        ...            
}});
```



## 3.全局API

- **选项模板**（很少使用）

  ```html
  <div id='app'></div>
  ```

  ```javascript
  new Vue({
      el:'#app',
      template:`<div>
  		<h1 style="color:red">选项模板 自动挂载</h1>
  	</div>`
  })
  ```

- **标签模板**

  ```html
  <div id='app'></div>
  <template id='tep'>
  	<h1 style="color:blue">标签模板 自动挂载</h1>
  </template>
  ```

  ```JavaScript
  new Vue({
      el:"#app",
      template:"#tep"
  })
  ```

- **script标签模板**

  ```html
  <div id="app"></div>
  ```

  ```javascript
  <script type="text/x-template" id="tpl">
  	<div>
      	<h1 style="color:green">script标签模板 自动挂载</h1>
      </div>
  </script>
  <script>
  	new Vue({
  		el:"#app",
          template:"#tpl"
      })		
  </script>
  ```

  

- **组件传值**

  （父子组件的概念，组件中data的类型必须为函数类型）

  **props**：子组件通过props获取父组件中的值（类型为数组或者对象）
  
  父组件里面可以嵌套子组件
  
  
  
- **component切换组件**

  ​	通过Vue中的component标签的 is:特性来实现多个组件之间的切换

  ```html
  <div id="#app">
      <a href="#" @click="clickName='login'"> 登录 </a>
      <a href="#" @click="clickName='register'"> 注册 </a>
      <a href="#" @click="clickName='password-retake'"> 找回密码 </a>
  </div>
  <script>
  	Vue.component(
      	"login",
          {template:`<h2 style="color:red">登录组件</h2>`}
      ),
      Vue.component(
      	"register",
          {template:`<h2 style="color:green">注册组件</h2>`}
      ),
      Vue.component(
      	"password-retake",
          {template:`<h2 style="color:blue">找回密码组件</h2>`}
      )
      new Vue({
          el:'#app',
          data:{
              clickName:'login'
          }
      })
  </script>
  ```

  

- **Vue.version**

  查看当前Vue 的版本号



**注：**在vue中可以嵌套使用jQuery库（ajax请求，Premise异步操作等）



## 4.数据api

后面补充.....



## 5.安装Vue脚手架构建工具与使用

**注：**安装vue脚手架的前提是在node环境下安装（即存在node即包管理工具npm/cnpm）



- 淘宝镜像( cnpm )安装：npm i -g cnpm --registry=https://registry.npm.taobao.org

  

- 全局安装webpack：cnpm i webpack webpack-cli -g

  - 查看版本：webpack -v   |    npm view webpack-cli



- 全局安装vue-cli：cnpm i vue-cli -g    ( vue2.x版本 )

  ​	项目初始化：	vue init webpack 项目名称

  ​	项目运行：npm run dev （注：必须进入当前文件夹）

  

- vue2.x与vue3.x共存：cnpm i -g @vue/cli-init（防止3.x版本覆盖2.x版本）

  

- 全局安装vue-cli：cnpm i -g @vue/cli （ vue3.x版本 ）

  ​	项目初始化：vue create 项目名称，后面按照提示进行选择配置

  ​	项目运行：npm run serve
  
  
  
- 打开vue图形界面：vue ui  （在任何地方都可以通过该命令进入）

  

- 查看当前全局vue-cli版本：npm view vue-cli

  

- 查看当前全局vue版本：vue -V ( --version ) 

  

  
  

## 6.vue生命周期

**定义：**从Vue实例创建、运行、到销毁的过程中，会伴随着一些各种类型的事件，这些事件统称为生命周期

**生命周期的过程（三大阶段，十小步）**

​	注：需要监听什么组件的生命周期就把函数放在该组件中

- `创建期间的生命周期函数`
  - beforeCreate()    —— **创建前**（数据绑定前）
    - 实例刚在内存中被创建出来，此时还没有初始化好 data 和 methods 属性
  - created()    —— **创建完成**（数据绑定完成）
    - 实例已经在内存中创建ok，此时 data 和 methods 已经创建ok，但没没有开始编译模板（视图）
  - beforeMount()    —— **即将挂载**
    - 已经完成了模板的编译，但是还没有挂载到页面中
    - 到这一步的时候开始异步加载其他组件，直到模板编译完成才执行下一步
  - mounted()    —— **挂载完成**
    - 此时已经将编译好的模板，挂载到了页面指定的容器中显示
- `运行期间的生命周期函数`
  - beforeUpdate()    —— **更新前**（即将更新）
    - 状态更新之前执行此函数，此时 data 中的状态值是最新的，但是页面上显示的还是更新之前的数据，因为此时还没有开始重新渲染DOM节点
  - updated()    —— **更新完成**
    - 实例更新完毕之后调用此函数，此时 data 中的状态值和页面上显示的数据都已经完成了更新，页面已经被重新渲染完成
  - activated()    —— **激活时**
    - keep-alive组件激活时调用
  - deactivated()    —— **停用时**
    - keep-alive组件停用时调用
- `销毁期间的生命周期函数`
  - beforeDestory()    —— **销毁之前**（组件销毁之前调用）
    - 实例销毁之前调用，此时实例依旧可以使用
  - destoryed()    —— **销毁完成**
    - Vue实例销毁之后调用，调用后，Vue实例指示的所有东西都会解绑，所有事件监听器会被移除，所有的子实例也会被销毁



**生命周期图示**



## 7.Vue常用UI组件库

​	**注**：一般在实际项目开发中根据设计图或者需求选择一两个组件库使用就行，并且在项目开始之前就要确定好使用什么组件，提前安装，会重写App.vue和main.js文件

### Vant

​	 `轻量、可靠的移动端Vue组件库`

​	 官网：https://youzan.github.io/vant/#/zh-CN/intro

​	**文件配置**：在bable.config.js文件中添加配置

​	**按需引入组件**：import {xxx} from "vant"	（ 因为需要在一个项目中的多个子页面或者组件中使用，故在main.js文件中引入 ）

​	**注册组件**：vue.use(xxx).use(xxx2).use(xxx3)  （链式操作）



### iView

​	`基于vue.js的开源PC端UI组件库`

​	 官网：https://www.iviewui.com/

​	**注**：vue-cli3.0以下使用npm命令安装，3.x版本可以在图形界面中的插件安装，先使用`npm install iview --save`安装模块

​	`组件引入方式`：

- 全局引入，直接在main.js文件中添加（不需要引入样式文件及注册组件）

  ```JavaScript
  import './plugins/iview.js'
  ```

- 局部引入，按需在某个组件页面中引入（需要引入样式文件以及注册解构的组件）

  ```js
  import {xxx1,xxx2,xxx3} from 'iview';
  import 'iview/dist/styles/iview.css';
  
  data(){
      return {
          components:{
              xxx1,xxx2,xxx3
          }
      }
  }
  ```



### Element

​	`Element，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库`

​	官网：http://element-ui.cn/#/zh-CN



## 8.组件及文件的引入方法及其他问题

- **引入组件**

​	import  ( 用一个变量名代替 )  from   文件路径 ：变量名最好能够见名知意，组件名使用驼峰命名

如：impirt HelloWorld  from  '../components/HelloWorld.vue'



- **引入图片等文件的多种路径**（<font color="red">**重**</font>）

  - `在html中引入`

    ```html
    <img src="相对(绝对)路径" alt="" >
    ```

  - `在js中引入`

    ```javascript
    <img :src="img" alt="">
    
    <script>
    	export default {
            data(){
                return {
                    img:require('../../public/static/images/1.jpg')
                }
            }
        };
    </script>
    ```

  - " / " 在vue项目中表示根路径，即public文件夹，静态资源均放在 public 下的 static 目录中

  - " @ " 在vue项目中表示 src 目录，可以将文件放在 src 目录下的 assets 文件夹中

  - `在 css 中引入`

    ```html
    <style>
    	@import url("../assets/css/c.css")
    </style>
    ```

  - " ~ " 在vue项目中表示node_modules 文件目录，可以引用其中的文件

    

- `解决引入第三方js插件出现未定义的问题`

  ​	导入第三方插件时出现 xxx not defined 时需要在项目根目录下创建一个  **vue.config.js** 文件，并手动添加以下代码

  ```JavaScript
  module.exports = {
      configureWebpack: {
          externals: {
              "md5": "md5"
          }
      },
      // 还可以导出其他第三方插件
  }
  ```

  

- `vue-cli3.x 跨域问题`

  ```JavaScript
   devServer: {
          open:true,
          // port:8088,
          // 配置跨域
          proxy: {
              '/api':{			// 随便一个名字
                  traget:'http://localhost/echotest.php',
                  changeOrigin:true
              }
          }
        }
  ```




## 9.eventBus（事件车）及图片预览

​	`eventBus`是一种发布/订阅-设计模式的实践，主要用于**跨组件之间的通信**，但仅局限于简单的组件页面场景，很多大型组件页面的通信（如购物车）需要使用 `VueX` 进行状态管理

图示：

![](F:\Web前端\js第九期-系统班\第三阶段-vue\个人学习笔记\追梦-vue\08-事件车（实现数据共享）\eventBus.png)

实例：（兄弟组件之间通信依赖于父组件）

```javascript
// 在src的utils目录下创建eventBus.js文件

import Vue from 'vue'
export default new Vue()
```

​	子组件A：

```html
<template>
	<div>
        <h1>{{num}}</h1>
        <button @:click='sendData'>点击发送数据</button>
    </div>
</template>

<script>
    import Bus from '@/utils/eventBus'
	export default {
        name:'A',
        data(){
			return {
                num:0
            }
        },
        methods:{
            /*
            	使用 $emit 来发射数据
            	上车（将A组件中的数据携带到eventBus上）
            */ 
            sendData(){
               	Bus.$emit('send',++this.num)
            }
        }
    }
</script>
```

​		子组件B：

```html
<template>
	<div>
        <h1>{{count}}</h1>
    </div>
</template>

<script>
	import Bus from '../utils/eventBus'
    export default {
        name:'B',
        data(){
            return {
                count:0
            }
        },
       created(){
           /*
           		通过 $on 来监听发送过来的数据
           		注：因为在点击之前this指向B组件的实例，但在点击之后就是指向Bus的Vue实例了，故此处回调函数需要使用箭头函数来让this指向B组件
           		下车（eventBus中的数据传递到B组件）
           */
           Bus.$on('send',(v)=>{
               this.count = v
           })
       }
    }
</script>
```

​	

**图片预览**

​		`vue2-preview ` 模块支持图片预览，需要安装对应的模块

​		[vue2-preview](https://www.npmjs.com/package/vue2-preview)

​		**Vant** ui组件库中也可以实现图片预览



## 10.Vue Router

​	`Vue Router` 是 Vue.js 官方的路由管理器，能够让构建单页面应用变得更加简单

- 路由匹配优先级

  ​	有时候同一个路径可以匹配多个路由，匹配规则就是谁先定义谁的匹配优先级就越高（从上到下）

  

- 捕获所有路由或者404路由

  ​	常规参数只会匹配被 `/` 分隔的 URL 片段中的字符。如果想匹配**任意路径**，我们可以使用通配符 (`*`)

  ​	注：当使用*通配符*路由时，请确保路由的顺序是正确的，也就是说含有*通配符*的路由应该放在最后，**当path值为空时（空的子路由）会渲染该组件**

  ​	

- `path`是大家在浏览器网址中看到的路径，在 vue 中建议使用 `name`属性去匹配，类似react中的精准匹配

  ​	**注**：path属性是必须添加的（呈现给用户的地址）
  
  ```html
  <!-- 1.path属性匹配 -->
  <router-link to="/">Home</router-link>
  
  <!-- 2.name属性匹配 -->
<router-link v-bind:to="{name:'about'}">About</router-link>
  ```
  
  
  
- `路由嵌套`

  ​	在实际应用中，路由嵌套是很常见的，有时候还会嵌套多级路由

  ```JavaScript
  {
      path:'/',			// 一级路由（主路由）
      name:'home',
      component:Home,
      children:[			// 子路由配置项 需要使用<router-view />路由容器来显示对应的组件
          {
              path:'/home/news',		// 二级路由（子路由）
              name:'news',
              component:News
          },
      ]
  }
  ```

  ​	**注**：子路由显示在什么地方？即在需要显示的地方添加一个 `<router-view />` 路由容器来装载对应的子路由组件 

  

- `路由传参`

  ​	在路由中，我们需要通过传参来异步请求后端接口，获取数据来渲染当前页面组件

  - 路径参数（params）（动态路由参数）

    ```html
    <router-link to="/home/news/xxx">新闻</router-link>
    
    {
    	path:'/home/news/:id'
    	component:News
    }
    <!-- 通过this.$route.params获取参数 -->
    ```

  - 字符串查询参数（query）

    ```html
    <router-link :to="{name:news},query:{xxx}"
                 
    <!-- 通过this.$route.query获取参数 -->
    ```

  - 二者都通过 `this.$route` 来获取参数的（生命周期中使用，一般用在mounted，或者其他生命周期函数）

  

- `编程式导航`

  ​	<font color="red">编程式导航</font>即通过编写代码来实现路由跳转。在路由匹配时，有时候我们无法用到`<router-link />`作为 a 标签进行路由跳转，这时就可以使用编程式导航进行路由跳转（还可以实现路由重定向）

  语法：在Vue实例内部

  ```JavaScript
  /*
  	方法一：router.push()，参数可以是一个字符串路径，也可以是一个描述地址的对象
  		特点：会向history栈中添加一条新的记录，当用户点击浏览器后退时会回到之前的url
  */
  this.$router.push(url)
  /*
  	方法二：router.replace(),参数可以是一个字符串路径，也可以是一个描述地址的对象
  		特点：不会向history栈中添加新的记录，会替换到当前history中的记录		
  */
  ```

  
  
- `路由重定向和别名`

  ​	**重定向 **指用户访问一个 url 时会被替换到另一个 url
  
  ```JavaScript
  // 方法一
  {path:'/home',redirect:'/home/news'}    // 重定向到 /home/news 路由
  
  // 方法二
  { path: 'home', redirect: { name: 'music' }} 	// 重定向到name为music的路由
  
  // 方法三
  { path: '/a', redirect: to => {
        // 方法接收 目标路由 作为参数
        // return 重定向的 字符串路径/路径对象
  }}
  // 方法四
  created(){
      this.$router.replace('/music')		// 使用编程导航的方法重定向路由
}
  ```
  
  ​		**别名** 指用户访问一个 url 时会被该 url 的另一个名字代替，但还是匹配到原来的 url 上
  
  ```JavaScript
  {path:'/home/music' component:Music alias:'/xxx' }  // 即'/xxx' 代替了 '/home/music'
  ```
  
  

## 11.路由管理

- `文件引入方式`

  ```javascript
  //绝对路径
  // 1.在项目运行目录 public（/）下引入
  <img src="/xxx.png" alt="">
  
  //相对路径
  // 2.直接引入
  <img src="../xx/xxx.png" alt="">
      
  // 3.作为模块引入（import）
  <img :src="img" alt="">
  <script>
  	import pic from '../xx/xxx.png'
  	export default {
          data(){
              return {
                  img:pic
              }
          }
      }
  </script>
  
  // 4.require方式引入
  <img :src="img1" alt="">
  <script>
  	export default {
          data(){
              return {
                  img1:require('../xx/xxx.png')
              }
          }
      }
  </script>
  ```

  

- `路由（导航）守卫`

  ​	正如其名，`vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的

  - <font color="lime">**全局守卫（会对所有路由组件生效）**</font>

    ​	使用`router.beforeEach` 注册一个全局前置守卫，

    ```JavaScript
    router.beforeEach((to,from,next)=>{
    	/*
    		to:表示即将要去的路由
    		from:表示当前导航正要离开的路由
    		next:接收一个函数表示来执行上面的操作（结合判断使用）
    		注：其中to和from都为一个路由对象
    	*/   
    })
    
    ```

    ​	使用`router.afterEach` 注册一个全局后置钩子

    ```JavaScript
    router.afterEach((to,from)=>{
        // 和前置守卫不同的是不会接收next函数，也不会改变导航本身
    })
    ```

  - <font color="lime">**路由独享守卫**</font>

    ​	使用`beforeEnter` 定义一个路由独享守卫，顾名思义，是对设置的某个路由组件生效

    ```JavaScript
    beforeEnter:(to,from next)=>{
        ......
    }
    //es6语法
    beforeEnter(to,from,next){
        ......
    }
    ```

  - <font color="lime">**组件内的守卫**</font>

    ​	可以在路由组件中定义 `beforeRouteEnter`，`beforeRouteUpdate`，`beforeRouteLeave` 三种路由导航

    ```javascript
    beforeRouteEnter(to,from,next)=>{
    	/*
    		由于该守卫是在确认之前被调用，但是目标组件还未被创建，故不能使用 this 实例对象，可以给next传递一个回调函数来访问实例：next(vm=>{ ... })
    		唯一支持给next传递回调函数的钩子，后面两种不支持，也没必要，因为已经能够使用 this 组件实例
    	*/
    },
    beforeRouteUpdate(to,from,next)=>{
    	/*
    		在当前路由改变，但是组件被复用时调用，可以访问 this 组件实例
    	*/
    },
    beforeRouteLeave(to,from,next)=>{
    	/*
    		导航离开对应组件时调用，可以访问 this 组件实例
    		这个离开守卫通常用来禁止用户在还未保存修改前突然离开。该导航可以通过 next(false) 来取消
    	*/
    }
    ```

  - <font color="lime">**完整的路由导航解析流程**</font>

    1. 导航被触发
    2. 在失活的组件里调用离开守卫
    3. 调用全局的 `beforeEach` 守卫
    4. 在重用的组件里调用 `beforeRouteUpdate` 守卫
    5. 在路由配置里调用 `beforeEnter` 
    6. 解析异步路由组件
    7. 在被激活的组件里调用 `beforeRouteEnter` 
    8. 调用全局的 `beforeResolve` 守卫
    9. 导航被确认
    10. 调用全局的 `afterEach` 钩子
    11. 触发DOM更新
    12. 用创建好的实例调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数 

    

## 12.Vuex状态管理

​		`Vuex` 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

​		`Vuex` 包含三大部分：**state**：驱动应用的数据源；**view**：以声明方式将数据映射到视图；**actions**：响应在view上的用户输入导致状态变化

​		<font color="red">*单向数据流*</font> 工作原理图：

![](https://vuex.vuejs.org/flow.png)

​		问题：当实际项目中遇到多个组件共享状态时，就会破坏 `单向数据流` : 1.多个视图依赖于同一个状态；2.来自不同视图的行为需要变更同一状态



​		解决：把组件的共享状态提取出来，以一个全局单例模式管理，在该模式下，组件树就构成了一个巨大的 “视图”，不管在树的哪个位置，任何组件都能够获取状态或者触发行为！



​		通过定义和 <font color="red">*隔离状态管理*</font> 中的各种概念并通过强制规则维持视图和状态间的独立性 ——**Vuex基本思想**



​		使用 `Vuex` 的场景：Vuex 可以实现管理状态共享，并附带了其他的概念和框架知识。在实际开发中如果不是开发大型单页面应用，建议不要使用 Vuex，小型应用可以使用 [store]([https://cn.vuejs.org/v2/guide/state-management.html#%E7%AE%80%E5%8D%95%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86%E8%B5%B7%E6%AD%A5%E4%BD%BF%E7%94%A8](https://cn.vuejs.org/v2/guide/state-management.html#简单状态管理起步使用)) 模式，构建中大型应用就需要考虑使用 Vuex 进行组件外部的状态管理了。



​			<font size="5" color="red" >**状态调用**</font>

```JavaScript
// store.js文件
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
    state: {
        name: 'hello vuex',
        count:130,
        list: [
            {
                id:1,
                title:'框架玩会了么？',
                completed:true
            },
            {
                id:2,
                title:'vuex状态管理学会了么？',
                completed:true
            },
            {
                id:3,
                title:'明天准备实战了么？',
                completed:false
            }
        ],
    },
    getters:{         // store自带的获取状态的api，可认为是store的computed属性
        num1(state){
            return ++state.count
        },
        num2(state){
            return state.count
        },
        completed(state){
            return state.list.filter(item=>item.id==3)
        }
    },
    mutations: {},
    actions: {}
})
```

- 直接在Vue实例外部调用

  ```html
  <h1>{{$store.state.name}}</h1>
  <h2>{{$store.state.count}}</h2>
  ...
  ```

- 在Vue实例内部通过 **this** 调用

  ```javascript
  computed:{
      name(){
          return this.$store.state.name
      },
      list(){
          return this.$store.state.list.filter(item=>item.completed)
      }
  }
  ```

  **注**：外部组件中使用的名字和 store.js中的名字最好要一样

  <font color="red">**扩展：**</font>

  可以使用 vuex 中的 `mapState` 方法对state进行简化

  ```JavaScript
  import {mapState} from 'vuex'
  // 参数为数组
  computed:mapState(['name','list'])
  
  // 参数为对象
  computed:mapState({
      name:state=> (return state.name),
      list(state){
          return state.list.filter(item=>item.completed)
      }
  })
  ```

- ### Getter

  ​	通过 vuex 提供的 getter 方法获取 state 中的数据（可认为是 store 的 computed 属性）

  ```javascript
  computed:{		// Vue实例中的computed
      num1(){
  		return this.$store.getters.num1
      },
      completed(){
          return this.$store.getter.completed
      }
  }
  // 然后再在标签中进行渲染
  
  // 使用 mapGetters 简化 getters
  computed: mapGetters(['num1','completed'])
  ```

  

- ### Mutation

- ### Action