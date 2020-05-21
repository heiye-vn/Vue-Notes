

# Vue Study Notes（Third Version）

## 1.认识vue

​	什么时vue?Vue是一个渐进式的框架  

什么是渐进式?    

​	1.渐进式:意味着可以将vue作为你的应用的一部分嵌入其中,带来更丰富的交互体验    

​	2.或者你希望更多的业务逻辑使用vue来实现,那么Vue的核心库以及其生态系统.     

​	3.Vue全家桶   vue vue-cli vue-router vuex axios 

## 基础写法

​	

```js
let vm = new Vue({
	el:"#app",	  //用于挂载元素
    data:{
        arr:[12,3,4],
        str:'乾坤',
        bool:false,
        fn(){
            return 123
        },
        ........
    }
 	
})

//如果按照以前的写法:
	  /*
        如果要是按照以前的js  (命令式)
              *   1.创建div 设置id
              *   2.定义一个变量
              *   3.把变量innHTML给这个div
              *   4.改变值
              *   5.改变后的值赋值回去
              * */

```

	## 指令:@click

​	v-on:click 或者 @click	

​		在 @click中 我们可以写方法  相当于   function handleradd(){    }		一般来说 如果不传入值的话,这个()是可以省略的  直接调用为    @clikc = 'handleradd'

​	什么是methods???  methods是一个方法.我们一般封装方法都在里面封装 封装的方法  调用的时候 是需要 fn()调用 但是在@click里不传入参数的话 ()是可以省略的 切记.

在methods里封装的方法  this一般指向这个实例   比如 想要调用 data里的数据   vm.name 可以调用出 云烨 

在  handleradd中打印的话 也是云烨 说明他指向 vm  

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../scr/vue.js"></script>
</head>

<body>
    <div id="app">
        <h2>{{counter}}{{con}}</h2>
        <!-- <button @click="con--">-</button>
        <button @click="con++">+</button> -->
        <button @click="handleradd">+</button>
        <button @click="handlerjian">-</button>
    </div>
    <script>
        /**
         * 指令  :  v-on:click  或者 @click
         * 
        */
        let vm = new Vue({
            el: '#app',
            data: {
                counter: '当前计数',
                con: 0,
                name:'云烨'
            },
            methods: {          //放置方法的
                handleradd() {
                     console.log(this.name) 
                    this.con++
                },
                handlerjian(){
                    this.con--
                }
            },
          

        })
    </script>
</body>

</html>
```

## 2.vue的options

el: 可以传入  string  HTMLElement 

​		作用:决定vue的实例会管理哪一个dom 

data:可以传入  Object  Function(组件当中data必须是一个函数) 

​		 作用:vue的实例对应的数据对象 
 methods: 可以传入 [key:string:function] 

​	 	作用:定义一些vue的方法 可以再其他地方调用,也可以再指令中调用

created:传入网络请求

 filters  过滤器

## 3.插值

​	什么是插值?

​		{{}} 称之为Mustache语法  不仅仅可以学语法,还可以学简单的表达式

​			比如字符串的拼接  数字相乘等等一系列

例如:

```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>

<body>
  <div id="app">
    {{msg}} <br>			
    {{msg+agg}} <br>	
    {{msg+''+agg}}  <br>
    {{counter}} <br>
    {{counter*2}}
  </div>
  <script>
 
    let vm = new Vue({
      el:'#app',
      data:{
        msg:'乾坤',
        agg:'筱湘',
        counter:100,
      }
    })
  </script>
</body>

</html>
```

## 指令v-once

​		当元素只渲染展示一次的时候

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      {{msg}}
      <h2 v-once>{{msg}}</h2>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
        }
      })
    </script>
</body>
</html>
```

## 指令v-html, v-text,v-pre

​	v-html用于解析标签 和 innerHTML作用一样

​	v-text用于将标签内容完整输入出来.(一般不用 不够灵活) 和innerTEXT作用一样

​	v-pre用于把标签内容原封不动的显示出来.不做任何解析

## 指令v-cloak

​	在vue解析之前div中有一个v-cloak 

​	在vue解析之后div中没有v-cloak

​	????这个有啥用..

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
  <style>
      [v-cloak]{
        display: none;
      }
  </style>
</head>
<body>
    <div id="app" v-cloak>
      {{msg}}
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
        }
      })
    </script>
</body>
</html>
```

## v-bind(1)

​	v-bind是动态绑定属性   通常语法糖写法为  :	

​			标签内的自带属性都可以加 :   来实现动态绑定的效果比如   img的 widht height

​	用这个的话 便于项目维护 而不用去更改html代码 

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <!--再这里不能使用mustache语法-->
      <img v-bind:src="imgurl.url" v-bind:width="imgurl.width" >
      <a :href="hrefs.aHref">我是链接</a>
     
    </div>
    <script>
 
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          imgurl:{
            url:'./图片/1.png',
            width:500,
            height:500,
          },
          hrefs:{
            aHref:'http://www.baidu.com'
          }
        }
      })
    </script>
</body>
</html>
```

## v-bind(2)对class的动态绑定

​		可以直接绑定   比如   :class="active"

​	也可以通过boolean来控制

​				:class="{类名1:boolean,类名2:boolean}"

​	这些class最后会合并成为   class=" 类名1   类名2"

watch属性:

​		用来监听data里的数据的变化  

​			固定写法

​				你要监听的名称(){		}


```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
  .active{
    color: red;
  }
  .line{
    font-size: 50px;
  }
  </style>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
        <!-- <h2 :class="active">{{msg}}</h2> -->
        <!-- <h2 :class={类名1:boolean,类名2:boolean}>{{msg}}</h2> -->
        <h2 class="title" :class="{active:ifActive.text1,line:ifActive.text2}">{{msg}}</h2>   <!--这些class会合并-->
        <button @click="fn">按钮</button>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          ifActive:{
            text1:true,
            text2:true
          }

        },
        methods: {
          fn() {
            this.ifActive = !this.ifActive
          },
        },
        watch: {
          ifActive(newValue,) {
              console.log(typeof newValue, newValue);
              
          },
        },
       
       
        
      })
    </script>
</body>
</html>
```

### 以上方法也可以抽离出来 



```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
  .active{
    color: red;
  }
  .line{
    font-size: 50px;
  }
  </style>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
        <h2 class="title" :class="getclass()">{{msg}}</h2>   <!--这些class会合并-->
        <button @click="fn">按钮</button>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          ifActive:{
            text1:true,
            text2:true
          }

        },
        methods: {
          fn() {
            this.ifActive.text1 = !this.ifActive.text1
            this.ifActive.text2 = !this.ifActive.text2
          },
          getclass(){
            return {active:this.ifActive.text1,line:this.ifActive.text2}
          }
        },
        watch: {
          ifActive(newValue,) {
              console.log(typeof newValue, newValue);
              
          },
        },
       
       
        
      })
    </script>
</body>
</html>
```

## 

### v-bind还能是数组(当然 只是调用的data)



```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <h2 class="title" :class="[active,'line']">{{msg}}</h2>
      <h2 class="title" :class="fn()">{{msg}}</h2>
      <div :style="sty"></div>
    </div>
    <script>

      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          active:'cat',
          sty:{
            width:"100px",
            height:'100px',
            border:"1px solid green"
          }
        },
        methods: {
          fn() {
            return [this.active,'line']
          },
        },
      })
    </script>
</body>
</html>
```

### v-bind对style的绑定

```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>

<body>
  <div id="app">
    <!-- <h2 :style="{key(属性名):value(属性值)}"></h2> -->

    <!--50px必须加上单引号 不然解析为变量-->
    <h2 :style="{fontSize:'50px'}">{{msg}}</h2>
    <h3 :style="cssText"></h3>
    <h3 :style="getcsstext()"></h3>
  </div>
  <script>
    let vm = new Vue({
      el: '#app',
      data: {
        msg: '你好',
        cssText: {
          display: "block",
          width: "100px",
          height: "100px",
          border: "1px solid green",
          backgroundColor: "red"

        }
      },
      methods: {
        getcsstext() {
          return {
            display: "block",
            width: "100px",
            height: "100px",
            border: "1px solid green",
            backgroundColor: "red"

          }
        },
      },
    })
  </script>
</body>

</html>
```

### 绑定style的数组写法

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <h2 :style="[baseStyle,nodeStyle]">{{msg}}</h2>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          baseStyle:{fontSize:"100px"},
          nodeStyle:{color:'red'}
        }
      })
    </script>
</body>
</html>
```

## 计算属性	computed

method与computed

method是一个方法  里面的函数需要调用的时候执行 fn()执行

computed是属性  他可以直接用

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <h2>{{firstname+lastname}}</h2>
      <h2>{{getfullname()}}</h2>	//这里是methods里写的东西
      <h2>{{fullname}}</h2>		//这里直接使用计算属性写的东西
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          firstname:'清水',
          lastname:"乾坤"
        },
        //方法
        methods: {
          getfullname() {
              return this.firstname+''+this.lastname;
          },
        },
        //计算属性
        computed:{
          fullname(){
            return this.firstname +'' +this.lastname
          }
        }
      })
    </script>
</body>
</html>
```

如何使用呢?

### 案例



```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
       总价格:{{fullpir}}		//这里我直接调用computed里写好的方法 来计算出总价格
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          book:[
            {id:110,name:'暗渡',pirce:119},
            {id:111,name:'暗渡1',pirce:12},
            {id:112,name:'暗渡2',pirce:159},
            {id:113,name:'暗渡3',pirce:19},

          ]
        },
      computed:{
          fullpir(){
            let result = 0
              for(let i = 0;i<this.book.length;i++){
                  result +=this.book[i].pirce;
              }
              console.log(typeof result);
              
              return result;
          }
      }
      })
    </script>
</body>
</html>
```

### 计算属性中的setting和getting

​	一般在computed里写入一个方法 他是内置有两个默认的方法的 setting以及getting的

但是一般是没有set方法的,只读属性.我们都是在get里写东西 但是一般我们都是忽略get方法的 

```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>

<body>
  <div id="app">
    {{fullname}}
  </div>
  <script>
    let vm = new Vue({
      el: '#app',
      data: {
        msg: '你好',
        firstname: "qiankun",
        lastname: 'qingshui'
      },
      //一般是没有set方法,只读属性.
      computed: {
        fullname: {
          //如果非得有set:
          set(newValue){
            console.log("-------",newValue);
            //怎么保存这个newValue呢
            let nnams = newValue.split('');
            this.firstname = nnams[0],
            this.lastname = nnams[1];
            
          },
          get: function () {
            return this.firstname + this.lastname
          }
        },
        // fullname: function(){           省略了 get
        //   return this.firstname + this.lastname

        // }
      }
    })
  </script>
</body>

</html>
```

### 计算属性与methods的对比

methods会有缓存  computed只会调用一次就够了  提高了性能

```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>

<body>
  <div id="app">
    <!--直接拼接太繁琐-->
    {{fullname+lastname}} <br>
    {{fullname}} <br>
    {{fullname}} <br>
    {{fullname}} <br>		//控制台只打印一次
    {{fullname}} <br>
    {{fullname}} <br>
    {{getfullname()}}<br>
    {{getfullname()}}<br>		//打印4次
    {{getfullname()}}<br>
    {{getfullname()}}<br>
  </div>
  <script>
    let vm = new Vue({
      /**
        computed 只用调用一次就能用了 
        methode 会有缓存
      */
      el: '#app',
      data: {
        msg: '你好',
        firstname: "qiankun",
        lastname: 'qingshui'
      },
    
      computed: {
        fullname: {
        
          get: function () {
            console.log('getfullname')
            return this.firstname + this.lastname
          }
        },
       
      },
      methods: {
        getfullname() {
          console.log('我是meth的')
          return this.firstname + this.lastname
        }
      },
    })
  </script>
</body>

</html>
```

​	

## 指令 v-on() 如何传参

再定义事件的时候,写函数省略了小括号.但方法本身需要传入一个参数
如果函数需要参数,但是没有传入,那么函数的形参为undefined
再写事件函数的时候 没有加入小括号就会返回event

怎么才能有需要别的参数还有event参数  传入实参的时候需要些$event

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <button @click="handler1()">按钮1</button>
      <button @click="handler1">按钮2</button>
      <button @click="handler2()">按钮3</button>
      <button @click="handler2">按钮3.1</button>
      <button @click="handler3(1, $event)">按钮4</button>		//传入两个参数 1 ,even事件 需用$
      <button>按钮5</button>
    </div>
    <script>
 
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          countn:0,
        },
        methods: {
          handler1(){
            console.log(1);
            
          },
          handler2(abc){
            console.log(abc);
            
          },
          handler3(agt,e){
          console.log(agt,e);
          
          }
        },
      })
    </script>
</body>
</html>
```

### v-on修饰符

.stop  修饰符  加上久阻止冒泡    

.prevent   阻止默认事件              	

.once 给节点绑定一个一次性事件			

.stop 阻止事件冒泡			 			

.capture	事件捕获			 

.self 点击它的时候才会触发			

.prevent 阻止默认行为    

监听某个键帽      @keyup.(你需要要监听的键帽)*/



```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>

<body>
  <div id="app">
    <div @click="handler1">
      gar
      <div @click.prevent="handler2">
        fath
        <div @click.stop="handler3">
          son
        </div>
      </div>
    </div>
    <!--监听某个键盘的键帽---->
    <input type="text" v-on:keyup='keyup'>
  </div>
  <script>

    let vm = new Vue({
      el: '#app',
      data: {
        msg: '你好',
      },
      methods: {
        handler1() {
          console.log("gar")
        },
        handler2(){
          console.log('par');
          
        },
        handler3(){
          console.log('son');
          
        },
        keyup(){
          console.log(123)
        }
      },
    })
  </script>
</body>

</html>
```

## 指令 v-if

​	v-if

​	v-else-if

​	v-else

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
     <h2 v-if="isshow">{{msg}}</h2>
     <h2>{{msg1}}</h2>
    </div>
    <script>
  
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          isshow:'true',
          msg1:'不,我不好'
        }
      })
    </script>
</body>
</html>
```

### v-else(我们一般不这么写	

​		if-else  如果写在标签里会被打死 一般抽离出来

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <!-- <h2 v-if="score.score1>=90">优秀</h2>
      <h2 v-else-if="score.score1>=80">良好</h2>
      <h2 v-else-if="score.score1 >=70 ">还可以</h2>
      <h2 v-else>不及格</h2> -->
      <h2>{{result}}</h2>		//抽离写法
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          score:{
            score1:70
          }
        },
        computed:{
          result(){
              let showresult = '';
              if(this.score.score1>=90){
                showresult = '优秀'
              }else if(this.score.score1>=80){
                showresult = '不错'
              }else if(this.score.score1>=90){
                showresult = '不错'
              }else{
                showresult = '不及格' 
              }
              return showresult;
          }
        }
      })
    </script>
</body>
</html>
```

## 指令v-for

​	遍历数组有两个值   (item,idx)	(值本身,下标)	

​	遍历对象有三个值 (value,jian,idx)	(值,键.下标)

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <ul>
        <li v-for="(item,idx,sel) in msg" >{{item}}---{{idx}}----{{sel}}</li>
      </ul>
    </div>
    <script>
  
      let vm = new Vue({
        el:'#app',
        data:{
          msg:{
            name:'qianun',
            age:'18',
            height:'180cm'
          },
        }
      })
    </script>
</body>
</html>
```

###  key值

​	v-for 使用过程添加  :key           splice()数值中间插入元素    splice(2,0,f)我们希望给BC之间插入一个F.Diff算法默认执行起来是这样的:  即把C更新为F D更新为C ...依次往后更新 这样很没有效率  所以我们需要使用key来给每一个节点做一个唯一的标识    diff算法就可以正确的识别此节点    找到正确的位置插入新的节点    

所以 一句话  key的作用主要是为了高效的更新虚拟DOM

:key="(  val  /   idx)	" 这里可以是下标 可以是值 任意一个  是你for 循环取的名字

```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>

<body>
  <div id="app">
    <ul>
      <li v-for="(item,idx) in msg" :key="item">{{item}}-----{{idx}}</li>
    </ul>
  </div>
  <script>

    let vm = new Vue({
      el: '#app',
      data: {
        msg: ['A', 'B', 'C', 'D', 'E']
      }
    })
  </script>
</body>

</html>
```

### 数据响应式



```js
数据是响应式的  vue内部会监听我们数据的变化
  当数组的方法更改会触发响应的
      push()最后一位增加
      pop()最后一位开始删除
      shift()删除第一位开始
      unshift() 数组最前面添加元素
      splice() 这个既可以删除 也可以删除  也可以替换 
      splice(start,long) start从哪个位置开始  
                  如果是删除 第二个参数传入你要删除几个元素 如果没有传入 就删除后面全部元素
                  如果是替换  第二个参数写替换的个数 然后增加你要替换的元素 
                   如果是插入 第二个参数为0 然后增加你要插入的元素 
       sort()  //排序 
       reverse() //反转数组
    
  Vue.set(要修改的对象,索引,修改后的值)
```

## 指令v-model(1)

v-model 一般用来绑定表单 来实行双向绑定的效果 当我改变我data的值的时候 绑定的value也随之改变

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <input type="text" v-model="msg">{{msg}}
    </div>
    <script>

      let vm = new Vue({
        el:'#app',
        data:{
          msg:null,
        }
      })
    </script>
</body>
</html>
```

### 原理

​	在实现双向绑定的时候 其实就是 监听我们输入的值 在js中是   e.target.value  实时监听 在输入出来

​	在vue中就是 v-on:input  这个指令来给当前元素绑定input事件	然后 这个事件调用一个我们封装的方法 

​	然后显示出来 

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <!-- <input type="text" v-model="msg">{{msg}} -->
          //原理
      <input type="text" v-on:input = 'valuechange'>{{msg}}
    </div>
    <script>

      let vm = new Vue({
        el:'#app',
        data:{
          msg:null,
        },
        methods: {
          valuechange(e){
            console.log(e);
            //input事件
            this.msg = e.target.value;
          }
        },
      })
    </script>
</body>
</html>
```

### v-modle与选择 

将上下值动态绑定 当我点击上面选项的时候 在下面显示出来

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
   
        <input type="checkbox" value="篮球" v-model="hobby">篮球
        <input type="checkbox" value="排球"  v-model="hobby">排球
        <input type="checkbox" value="乒乓去"  v-model="hobby">乒乓去
        <input type="checkbox" value="练习生"  v-model="hobby">练习生
      <h2>宁的爱好是{{hobby}}</h2>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          hobby:[],
        }
      })
    </script>
</body>
</html>
```

### v-modle与selet

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <!--1.选择一个-->
      <select name="" id="" v-model="fruit">
        <option value="苹果" >苹果</option>
        <option value="粒子" >粒子</option>
        <option value="香蕉" >香蕉</option>
        <option value="猴子" >猴子</option>
      
      </select>
      <h2>宁选择的水粿为:{{fruit}}</h2>

        <!--1.选择多个-->
        <select name="" id="x" v-model="fruits" multiple>  <!--multiple--> 按住ctrl可以一次性选择多个
            <option value="苹果" >苹果</option>
            <option value="粒子" >粒子</option>
            <option value="香蕉" >香蕉</option>
            <option value="猴子" >猴子</option>
            <option value="猴子" >猴子</option>
            <option value="猴子" >猴子</option>
          
          </select>
          <h2>宁选择的水粿为:{{fruits}}</h2>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          fruit:null,
          fruits:null,
        }
      })
    </script>
</body>
</html>
```



### v-modle与checkbox



```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <h1>你真的要联系两年半么?</h1>
      <label for="tongyi">
        <input type="checkbox" id="tongyi" v-model="isargee" >同意协议
      </label>
      <h2>宁选择的是{{isargee}}</h2>
      <button :disabled="!isargee">下一步</button>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          isargee:null
        }
      })
    </script>
</body>
</html>
```

### v-modle与radio

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <label for="nan">男</label><input type="radio" id="nan" name="sex" value="男" v-model="sex">
      <label for="nv">女</label><input type="radio" id="nv" name="sex" value="女" v-model="sex">
      <h2>宁选择的性别为:{{sex}}</h2>
    </div>
    <script>
      /**
       *  结合radio类型
       *  
      */
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          sex:null,

        }
      })
    </script>
</body>
</html>
```

## v-modle的修饰符

	*  v-model 修饰符的使用

*  lazy: 输入完成在绑定
*  lazy: 输入完成在绑定
*  trim  清楚首位的空格

```js
  <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <input type="text" name="" id="a" v-model.lazy="msg">{{msg}}
      <input type="text" name="" id="c" v-model.number="msg1">{{typeof msg1}}
   
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          msg1:''
        }
      })
    </script>
</body>
</html>
```

### v-for与v-modle

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="../scr/vue.js"></script>
</head>
<body>
    <div id="app">
      <label for="" v-for="item in orgind" :key="item">
        <input type="checkbox" name="" id="" :value="item" v-model="hobby">{{item}}

      </label>
      <h2 >{{hobby}}</h2>
    </div>
    <script>
      let vm = new Vue({
        el:'#app',
        data:{
          msg:'你好',
          orgind:['篮球','排球','乒乓球','跪求'],
          hobby:[]
        }
      })
    </script>
</body>
</html>
```

# 组件化

什么是组件化?

 他提供了一种抽象,让我们开发出一个个独立可复用的小组件来构造哦我们的应用 

 任何的应用都会被抽像成一颗组件树 可以让代码更加方便阻止和管理.并且扩展性也更强. 

​		步骤: 

​			 	 1.创建组件构造器    Vue.extend() 

​				2.注册组件          Vue.component()   (component)组件     

​				3.使用组件          在vue实例作用范围内使用

以下代码注册的为全局组件	因为他不是在vm里注册的

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../scr/vue.js"></script>
</head>
<body>
<div id="app">
    <!--组件最基本的使用-->
    <myh></myh>
</div>
<script>
  /**
   *  可以重复使用代码
   *  1.创建组件化构造器对象
   *  2.注册组件
   *  3.使用组件
   * */
      //1.创建组件构造器对象
  let conc =  Vue.extend({
        template:`
              <div>
                 <h2>别管我,我能泵</h2>
              </div>`
      })
  //2.组测组件 (给组件起标签名字)  Vue.component('组件标签名字',组件构造器)
  Vue.component('myh',conc)
  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',

    }
  })

</script>
</body>
</html>

```

## 全局组件与局部组件

​	全局组件 在全局中创建而不是在vue实例里注册  这样意味着可以在多个vue的实例中使用.	

​	局部组件:	

​			在vue的实例 vm当中 注册

​			使用 components注册 

代码:

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../scr/vue.js"></script>
</head>
<body>
<div id="app">
    <cpn></cpn>
</div>

<script>
  //1.创建组件构造器
  let cpnc = Vue.extend({
        template:`<div>
                    <h2>
                        我真相啊
                    </h2>
                </div> `
  })
  //    注册组件(全局组件,意味着可以在多个Vue的实例下使用) 局部组件呢? 在实例当中使用
  //   Vue.component('cpn',cpnc);	//全局组件
  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    components:{
      //cpn使用组件时候的标签名  组件名:构造器	//局部组件
        cpn:cpnc
    }
  })
</script>
</body>
</html>
```

## 组件的语法糖写法

全局写法

```js
 //注册全局组件
  Vue.component('cpn1',{
    template:`
       <div>
         <h2>我是全局组件的语法糖</h2>
       </div>

          `
  })
```

局部写法

```js
 let vm  = new Vue({
    el:'#app',
    data:{

    },
    components:{
            //注册局部组件  '组件名字':{ template:``}
      'cpn2':{
        template: `
        <div>
            <h2>我是局部组件</h2>
        </div>`
      }
    }
  })
```

### 这样的话 不够灵活  我们可以使用抽离写法

​	两种抽离写法   

​				1.使用 template (常用)		一定要用id

​				2.通过script的写法 注意 一定要使用type="text/x-template



```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="../scr/vue.js"></script>

</head>
<body>
<div id="app">
    <cpn></cpn>
    <cdse></cdse>
</div>
<!-- 抽离写法-->
<!--通过script的写法 注意 一定要使用type="text/x-template"-->
<script type="text/x-template" id="cpn">
    <div>

        <h2>我是通过script的写法</h2>
    </div>
</script>
<!--template写法-->
<template id="cpns">
    <div>
        <h2>我是template的写法</h2>
    </div>
</template>
<script>
        //注册全局组件
        Vue.component('cpn',{
          template:'#cpn'
        })
  let vm  = new Vue({
    el:'#app',
    data:{

    },
    components:{
    "cdse":{
      template: '#cpns'
    }
    }

  })
</script>
</body>
</html>
```

## 在组件中的data为啥必须是函数?

​	 如果这个data不是个函数 那么每次调用组件的时候 都是指向一个data 会引起连锁反应 如果使用方法 那么他就会在每次调用的时候*    都开辟一个新的内存空间来调用他.

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cpn></cpn>


</div>
<template id="cpn">
  <div>
    <button @click="hendlersub">-</button>
    <span>当前计数:{{counter}}</span>
    <button @click="hendleradd">+</button>

  </div>
</template>
<script src="../scr/vue.js"></script>
<script>
  Vue.component('cpn',{		//全局注册
    template:'#cpn',
    data(){
      return {
        counter:0,
      }
    },
    methods:{
      hendleradd(){
        this.counter++
      },
      hendlersub(){
        this.counter--
      }
    }
  })
  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },

  })
</script>
</body>
</html>
```

## 组件通信

### 父传子

​	父传子需要使用  props

​	用     props['名字1','名字2']      取完名字. 使用组件的时候   :名字="父的data"	

​	也可以在使用的时候  prpos:{

​		名字:{
​		type:传入的类型限制,

​		default:'当不绑定父data的时候",

​		required:true		//别人给他必须传入值

​	}

}

代码:

```js
<!DOCTYPE html>
<html lang="en" xmlns:v-for="http://www.w3.org/1999/xhtml">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
 <div id="app">
    <cpn :cmover="msg" :cm2="cv"></cpn>
   <cpn :covers="cv"></cpn>

     </div>

 <template id="cpn">
   <div>
     <ul>
       <li v-for="item in cm2">{{item}}</li>
     </ul>
     <h2>{{cmesage}}</h2>
     <h2>{{covers}}</h2>
   </div>
 </template>
     <script src="../scr/vue.js"></script>
     <script>
       /**  父传子
        *
        * */
       let vm = new Vue({
         el:'#app',
         data:{
           msg:'你好',
           cv:['小泽','泷泽','麻衣']
         },
         components:{
           'cpn':{
             template:'#cpn',
             //父传入子  需要定义一个变量  使用的时候
             // props:['cmover','cm2'],
             props:{
                // wsuibianqude:Array    ///这么写可以对数据进行限制  String Number  Boolean Array Object  Date Function Symbol
               cmesage:{
                 type:String,
                 default:"我是默认的1",       //传入默认值
                 required:true              //别人给他必须传入的值

               },
               covers:{
                 type: Array,
                 default: ['我是默认数组2'], //2.5

               }
             },
             data(){
               return {
                 move:['海泽王','海扁王','龙族']
               }
             },

           }
         }

       })
     </script>
</body>
</html>
```

### 父传子1

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
 <div id="app">
  <cpn1 :cpn1de="msg"></cpn1>
</div>
 <template id="cpn1">
    <div>{{cpn1de}}</div>
 </template>
     <script src="../scr/vue.js"></script>
     <script>
       let vm = new Vue({
         el:'#app',
         data:{
           msg:['A','B','C'],
         },
         components:{
           'cpn1':{
             template:'#cpn1',
             props:['cpn1de']
           }
         }
       })
     </script>
</body>
</html>
```

### 父传子2当我不绑定父的时候

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cpn1 ></cpn1>
</div>
<template id="cpn1">
  <div>
    <h2>{{covse}}</h2>
   <h3>{{shuju2}}</h3>
  </div>

</template>
<script src="../scr/vue.js"></script>
<script>
  let vm = new Vue({
    el:'#app',
    data:{
      msg:['a','b','c','d'],
      str:'我是string',
      jso:{
        name:'qiankun',
        age:'18'
      }
    },
    components:{
      'cpn1':{
        template:'#cpn1',
        props:{
          //变量名字
          covse:{
            type:Array,
            default() {
              return ['我是默认的数组1']
            }
          },
          //类型是对象或者数组的时候,默认值必须是一个函数
          shuju2:{
            type: String,
            default(){
                return 'hello'
            },
          }
        }
      }
    }
  })
</script>
</body>
</html>
```

### 父传子 在props中的驼峰标识

​	在props中 不能使用驼峰命名法 但是可以 用-做分割

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cpn :shuju1="info" :childeren-mesge="msg"></cpn>
</div>
<template id="cpn">
  <div>
    <h2>{{shuju1}}</h2>
    <span>{{childerenMesge}}</span>
  </div>

</template>
<script src="../scr/vue.js"></script>
<script>

  let cpn = {
    template:'#cpn',
    props:{
      shuju1:{
        type:Object,
        default(){
          return {
            mesg:'你好'
          }
        }
      },
      childerenMesge:{
        type: String,
       default:'啊啊啊啊'
      }
    }
  }
  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
      info:{
        name:'qiankun',
        age:'18',
        tall:'180cm'
      }
    },
    components:{
      'cpn':cpn
    }
  })
</script>
</body>
</html>
```

### 子传父

```
  //第一个参数为事件名字(随便取),第二个为参数 发射的在组件用的时候v-on:事件名字
```

子传父需要通过事件  this.$emit("名字",'需要传的值')

使用组件的时候 @名字=父的方法(事件)接收

代码:

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
    //第二步
  <cpn @itemclick="cpnonclik"></cpn>
</div>
<template  id="cpn">
  <div>
    <button v-for="item in cat" @click="btnonclick(item)">{{item.name}}</button>
  </div>
</template>
<script src="../scr/vue.js"></script>
<script>
  let cpn = {
    template:'#cpn',
    data(){
      return {
          cat:[
            {
              id:1,
              name:'推荐'
            },
            {
              id:2,
              name:'推荐'
            },
            {
              id:3,
              name:'推荐'
            },
          ]
      }
    },
    methods:{
      btnonclick(its){
        //自定义事件
        //第一步
      this.$emit('itemclick','乾坤')       //第一个参数为事件名字(随便取),第二个为参数 发射的在组件用的时候v-on:事件名字
      }
    }

  }


  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    components:{
      cpn
    },
    methods: {
      //第三步
      cpnonclik(a){
        console.log('cpnonclik',a)
      }
    }
  })
</script>
</body>
</html>
```



### 父访问子

​		在父组件中 我们使用$chilren.要调用的方法

​		但是在真实开发中我们不用这个方法

​		$children在打台中是一个数组  所以 当原本数据变的时候.数组也就变了.所以不常用

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cps></cps>
  <button @click="btnClick">我是按钮</button>
</div>
<template  id="abs">
  <div>我是子组件</div>
</template>
<script src="../scr/vue.js"></script>
<script>
  /** 在父组件里 使用 $children .要调用的方法
   *  但是在真实开发中不用 $chilidren来拿属性
   *
   * */
  let cps = {
    template:'#abs',
    methods:{
      showMessage(){
        console.log('我是子组件的showMessage')

      }
    },
    data(){
      return{
        name:'我是子组件的name'
      }
    }
  }
  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    methods:{
      btnClick(){
        console.log(this.$children);
        // this.$children[0].showMessage();
        // this.$children[0].name;
        // console.log(this.$children[0].name)
        for (let key of this.$children){
          console.log(key.showMessage())
          console.log(key.name)
        }

      }
    },
    components:{
      cps
    }
  })
</script>
</body>
</html>
```

### 父访问子2

在真实开发中.我们使用 $ref 来访问   在使用的时候只需要在调用组件的时候  需要 ref="名"

​	在负组件中   this.$refs.a.方法()

​	例如  <cps ref="a">

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
    //使用
  <cps ref="a"></cps>
  <cps ref="b"></cps>

  <button @click="btnClick">我是按钮</button>
</div>
<template  id="abs">
  <div>我是子组件</div>
</template>
<script src="../scr/vue.js"></script>
<script>

  let cps = {
    template:'#abs',
    methods:{
      showMessage(){
        console.log('我是子组件的showMessage')

      }
    },
    data(){
      return{
        name:'我是子组件的name'
      }
    }
  }

  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    methods:{
      btnClick(){
          //访问子里面的的方法  
        console.log(this.$refs.a.showMessage())
      }
    },
    components:{
      cps
    }
  })
</script>
</body>
</html>
```

### 子访问父

​	$parent

​	this.$parent.age

如果想直接访问vm这个根的话 就可以直接  this.$root.msg

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
 <cps></cps>
</div>
<template  id="abs">
  <childs></childs>
</template>
<template id="childs">
  <div>
    <h2>我是子组件</h2>
    <button @click="btnClick">我是按钮</button>
  </div>
</template>
<script src="../scr/vue.js"></script>
<script>
  let childs = {
    template: '#childs',
    methods:{
      btnClick(){
        //访问父组件
        console.log(this.$parent.age)
        //访问根组件
        console.log(this.$root)
      }
    },

  }
  let cps = {
    template:'#abs',
    components: {
      childs
    },
    data(){
      return{
        age:'我是cps的组件'
      }
    }


  }

  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    methods:{
      btnClick(){

      }
    },
    components:{
      cps
    }
  })
</script>
</body>
</html>
```

## 插槽	slot

slot 插槽 

  让使用者决定我们展示什么东西  让组件更具扩展性

 插槽的基本使用 <slot><slot>      

如果有默认值 <slot><button></button></slot>

  如果有多个值同时放入组件中进行替换时,一起作为替换元素 



```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cpn><button>我是我写的</button></cpn>
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>

</div>
<template  id="cpn1">
  <div>
    <h2>我是组件哈哈哈</h2>
    <button>淦</button>
    <!--可以写入默认值-->
    <slot><span>我是默认的</span></slot>		//插槽
  </div>
</template>
<script src="../scr/vue.js"></script>
<script>

  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    components:{
      'cpn':{
        template:'#cpn1',
      }
    }
  })
</script>
</body>
</html>
```



## 具名插槽

​	具名插槽可以选择你给哪个具体的插槽改变值.而不是一个改变 全部改变   	只是需要给插槽加入一个name

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cpn><button>我是插槽的东西</button></cpn>
  <cpn><span slot="cen">我是中间的</span></cpn>


</div>
<template  id="cpn1">
  <div>
    <h2>我是组件哈哈哈</h2>

    <!--可以写入默认值-->
    <slot name="left"><span >左</span></slot>	//给插槽起名字
    <slot name="cen"><span>中</span></slot>
    <slot name="right"><span>右</span></slot>
    <slot>哈哈哈</slot>

  </div>
</template>
<script src="../scr/vue.js"></script>
<script>


  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    components:{
      'cpn':{
        template:'#cpn1',
      }
    }
  })
</script>
</body>
</html>
```



## 编译的作用域	

​	什么是编译的作用域?

​		总结来说 你在哪个模板里用就是哪个模板的变量里找 比如 你在app这个模板里 就是找vm的变量

虽然都是isshow  但是一个是属于子 一个属于父

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">

<csdn v-show="isshow"></csdn>
</div>
<template id="cs">
 <div>
   <h2>我是子组件</h2>
   <button v-show="isshow">我是个按钮啊</button>
 </div>
</template>
<script src="../scr/vue.js"></script>
<script>
  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
      isshow:true
    },
    components:{
     csdn:{
        template:'#cs',
       data(){
          return{
              isshow:false
          }
       }

      }
    }
  })
</script>
</body>
</html>
```



## 作用域插槽

```
/** 作用域插槽
 *        父组件替换插槽里面的标签,但是内容又是由子组件提供的
 *        通过案例来阐明
 *            第一步 对这个slot 起名字  :你得名字="数据",
 *            第二部 使用组件的时候 需要在里面搞一个template  slot-scope="slot" 固定写法
 *            第三步  在temeplate 里使用  forin 这个 你起的名
 *
 *            总结: 父组件替换插槽的标签,但是内容由子组件提供.
 * */
```

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cps></cps>
//第二步
  <cps>
    <template slot-scope="slot">
        //第三步
      <span v-for="item in slot.qiankun" >{{item}}--</span><br>
      <span>{{slot.qiankun.join("*")}}</span>
    </template>
  </cps>

  <cps >
    <templatr slot-scope="slot">
<!--      <span v-for="item in slot.qiankun">{{item}}*</span>-->
    </templatr>
  </cps >
</div>
<template id="csdn">
  <div>
	//第一步
    <slot :qiankun="planglaunges">
      <ul>
        <li v-for="(item,idx) in planglaunges" :key="idx">{{item}}</li>
      </ul>
    </slot>

  </div>

</template>
<script src="../scr/vue.js"></script>
<script>

  let vm = new Vue({
    el:'#app',
    data:{
      msg:'你好',
    },
    components:{
      cps:{
        template:'#csdn',
        data(){
          return{
            planglaunges : ['javascript','java','c++','python','go','swift']
          }
        }
      }
    }
  })
</script>
</body>
</html>
```

# 模块化

前端的模块化规范 

​		Commnjs    AMD  CMD  es6的Modules

​	一般Commonjs在 node里使用的模块化



## es5的模块化

html文件

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">

</div>
<script src="../../scr/vue.js"></script>
<script>
  /**   为什么要模块化
   *    es5模块化
   * */

</script>
<script src="aaa.js"></script>
<script src="bbb.js"></script>
</body>
</html>

```

```js
/***
		aaa.js
/
;
var modleaaa = (function () {
    var name = '小明'
    var age = 18;
    var obj = {};
    function sum(num1,num2) {
        return num1+num2;
    }
    var flag = true;
    if(flag){
      console.log(sum(10,20))
    }
    obj.flag = flag;
    obj.sunm = sum;
    return obj;
})();
```

```js
/***
	bbb.js
*/
var c = modleaaa.sunm(11,2)
console.log(c)
```

### es6的模块化

html文件

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<!--如何解决命名冲突?-->
<!--我要怎么让ccc使用到aaa的变量?需要在aaa里导出 -->
<!--
    第一步给 script增加  type="module"
    第二步 给js文件写入   export{需要导出的东西}
    第三步 给需要使用的js文件导入  import

    或者 直接  export var num1 = 10000;
-->
<script src="bbb.js" type="module"></script>
<script src="aaa.js"  type="module"></script>
<script src="ccc.js"  type="module"></script>
</body>
</html>
```

aaa.js

```js
let names = '小明',
    age = 18,
    flag=true;

  function sunm(num1,num2) {
      return num1+num2;
  }
  if(flag){
    console.log(sunm(20,30))
  }
  //导出方式1
  export {
      flag,
      age,
      sunm,
  }
  //导出方式2
  export  let num3 = '凯旋';


//导出方式3 导出函数/类  或者使用第一种
  export function aj(num1,num2) {
      return num1+num2
  }
  export  function Fackus() {
    
  }
  export  class Person {
    run(){
      console.log('在奔跑')
    }
  }
  //导出方式4 export default    可以别人取名字
  //某些情况下 我们不需要别人取得名字  我们希望自己取名字 就需要这个了  切记  只能有一个
  const adddress = '北京欢迎你'
    export  default  adddress

//


```

bbb.js

```js
let names = '红',
    age = 18,
    flag=true;

function sunm(num1,num2) {
  return num1+num2;
}
if(flag){
  console.log(sunm(2,1))
}
  export  var num1 = 1000;
  export  let num2 = '乾坤';



```

ccc.js

```js
	/***
		接收
	*/ 
 import  {flag,sunm,Person} from "./aaa.js";
  import  {num1,num2} from "./bbb.js";
  //通过export default导入的时候是不需要大括号的.
  import  add from './aaa.js'

  if(flag){
    console.log('我是鬼才')
    console.log(sunm(100,200));
  }
  console.log(num1)
  console.log(num2)
  const p = new Person();
  p.run();
  console.log(add);

  //在导入东西非常多的时候
  import * as  duixiang from './aaa.js'
    let a =   duixiang.sunm(5,6);
  console.log(a)
```

# webpack配置与安装(需要node环境 )

​	我们一般使用webpack来实现

Webpack的安装与配置

​		可以直接  webpack ./src/main.js ./dist/bundle.js 不过这样很麻烦

配置:

准备工作 :

​			创建src文件夹  里面创建js 并列创建一个主窗口 mian.js. 创建css文件夹



1.现在终端中 进入这个文件夹  cd 文件夹

​	然后使用  webpack ./src/main.js ./dist/bundle.js 打包 

方法2:

1. 使用 终端 输入   npm.init  起名字  随便取  一直下一步  然后随便.xxx.js  然后一直下一步(回车) 

   出现package.json为成功

   2.创建一个js文件 名字为 webpack.config.js		

   ```js
   1.引入包   
   const path = require('path')
   module.exports = {
     entry:'./src/main.js',
     output:{
       path:path.resolve(__dirname,'dist'),
       filename:'bundle.js'
     }
   }
   //这个样子就能使用 直接使用 webpack
   ```

   

   3.在package.json中的 srcipt里 增加一行  "build":"webpack"  就可以使用npm run  build 进行打包了

   但是! 这样打包时调用的全局的 webpack 我们要如何才能不调用全局的 调用本地文件夹的呢?

   4.在终端中 输入 npm install webpack@3.6.0 --save-dev  这样就在项目文件夹里安装了一个局部的webpack

   在调用的时候就可以调用项目中的了 这样的好处在于不用害怕环境的webpack过于老旧 以调用本地的优先.

   5.如果有css文件 那怎么办?

   ​	这个时候就需要loder了

   ​	1.先把css文件与根入口js文件链接起来 	使用 require

   ```js
   require('./css/noramal.css');
   ```

   ​	2.导入loder 	 style-loader  css-loader

   ​	2.1在终端中导入  npm install style-loader --save-dev      npm install --save-dev css-loader

   ​	3.导入完成之后 在webpack.confing.js中写入

   ```js
   const path = require('path')
   module.exports = {
     entry:'./src/main.js',
     output:{
       path:path.resolve(__dirname,'dist'),
       filename:'bundle.js'
     },
       module:{
          rules: [
         {
           test: /\.css$/,
           use: [ 'style-loader', 'css-loader' ]
         }
       ]  
       }
   }
   ```

   

   ​	4.运行 npm run build  

   5.完成!					


.....以上后续见webpack项目 





## 总结+脚手架



​		为什么要模块化?

​				简单写js代码带来的问题

​				闭包引起的代码不可复用

​				自己实现了简单的模块化

​				AMD/CMD/CommonJS

​		ES6中的模块化使用

​			export

​			import

​	runtimecompiler与runtimeonly的区别

Vue程序运行过程  :

​	vm.options.template  -----(parse[解析])--->ast[抽象语法树]----------(compile[编译])------>vm.options.render(functions)

----------翻译成  virtual dom  -------------渲染成 ul





​	区别在于main.js

​	runtimecompiler:

​				他是通过 template --->ast --->render---->vdom -->ul

​	runtimeonly:  

​				他是直接通过  render  --->vdom -->ul

​	结论:

		1.  		runtimeonly的性能更高,代码量更小

render函数到底是个什么东西?
render函数到底是个什么东西?
render函数到底是个什么东西?
render函数到底是个什么东西?
render函数到底是个什么东西?

```js
render:function(createElement){
    //1.createElement('标签',{标签的属性},[''])
	//普通用法
		return createElement('h2'{class:"box"},['hello wrrld'])
    //进阶用法
		return createElement('h2'{class:"box"},['hello wrrld',createElement('<button>')])
      //怎么代替template
        return createElement(cpn)		//组件名
    	//也可以引用App
    render:function(h){
        return h(App)			
    }
    //简写 
    	render:h=>h(app)
    
    //这样的话就变成runtimeonly的写法了 
    //那么.vue文件中的template中的template被谁解析了呢
    在 vue的loader当中 使用的vue-template-compiler (webpack学习中的弟5节有提到 解析vue文件中)解析了
    
    
    
}
```



cli2的很多东西  在cli3里都隐藏了 如何才能看见呢?	

​		通过命令行   vue ui  可以进行配置与查看

如果你新建一个配置文件 需要  git commit -m '添加的文件'		只能取   vue.config.js

# 路由

```js
/**
 *  路由提供了两种机制 : 路由和传送
 *      路由是决定数据包从来源到目的地的的路径
 *      转送将输入端的数据转义到合适的输出端
 *   路由中有个非常重要的概念叫路由表
 *      路由表的本质上是一个映射表,决定了数据包的指向.
 *
 *
 */
/**
 *  什么是前端渲染  什么是后端渲染
 *
 *      什么叫后端渲染:
 *          早期使用 jsp?php等一系列进行
 *            传给服务器一个url  然后解析这个url  通过 html+css+java  java的作用实时从数据库中读取数据
 *            并且将它动态的放在页面.他在服务器直接已经生成了页面 然后传回给客户端最终的页面  他只有html+css
 *          当在点击跳转的时候 也会再给一个服务器一个url 然后继续通过 jsp技术进行后端渲染  然后返还给前端
 *              等等一系列
 *              这就形成了一个IO操作
 *      什么叫后端路由呢?
 *        后端处理URL和页面之间的映射关系
 *        总结:
 *            当我们页面中需要请求不同的路径内容的时候,交给服务器来来经行处理.服务器渲染好整个页面,并且将页面返回给
 *            客户端,这种情况下,渲染好的页面,不需要单独加载任何的js和css,可以直接交给浏览器展示.这样有利于seo优化
 *            缺点:
 *             一种情况是整个页面由后端人员来编写和维护
 *             另一种情况是前端开发人员如果要开发页面,需要通过php和java等语言来编写页面代码
 *             而且通常情况下 html代码和数据以及对应的逻辑会混合在一起,编写和维护都是非常糟糕的事情.
 *
 *      前后端分离阶段
 *        后端只提供数据,不负责任何阶段的内容.
 *          浏览器中显示的网页中的大部分内容.都是由前端写的js代码在浏览器中执行,最终渲染出来的网页
 *
 *         总结:
 *              随着ajax的出现,有了前后端分离的开发模式
 *              后端只提供api来返回数据,前端通过ajax获取数据 ,并且可以通过jacascript将数据渲染到页面中
 *              这样做最大的有点就是前后端责任清晰,后端专注于数据上,前端专注于交互和可视化上
 *              并且当移动端(ios,android)出现后,后端不需要任何处理,依然使用之前的一套api
 *              目前很多网站采用这种开发模式
 *
 *          第三段阶段  (SPA)单页面富应用阶段
 *            其实SPA最主要的特点就是在前端分离的基础上加了一层前端路由
 *             也就是前端来维护一套路由规则
 *             整个网站只有一个html页面
 *
 *            在一套的html+css+js是一套的全部的资源
 *            其就是由一个个组件 组成了一套的html+css+js
 *            当客户端请求的时候 就是请求的一套对应的组件  她不用刷新页面
 *            这些都是前端路由来控制的
 *            前端路由的核心
 *                改变url但是不刷新页面
 *
 *
 *                方法一: 改变哈希
 *
 *                    lacation.hash = ' foo'
 *
 *                 方法二: history
 *                    history.pushState({},'','foo')
 *
 *
 *                 history.back() 等价于 history.go(-1)
 *                 history.forward()等价于history.go(1)
 *
 *
 *
 *      步骤一:
 *            npm install vue-router --save
 *              (一般脚手架都选上了)
 *        步骤二:
 *            在模块化工程中使用它(因为是一个插件,所以通过Vue.use()来暗转路由功能)
 *            第一步:导入路由对象,并且调用Vue.use(VueRouter)
 *            第二步:创建路由实例,并且传入路由映射配置
 *            第三步:在Vue的实例中挂载创建的路由实例
 *
 *           步骤三  使用 vue-router
 *            第一步:创建路由组件
 *            第二部:配置路由映射,组件和路径映射关系
 *            第三步:使用路由:通过<router-link>和<router-view>
 *
 *
 *
 *
 *
 *
 *
 *
 *
 *
 *
 *
 */

```

## cl4如何操作	

路由组件在view里创建

​		第一步 先创建 比如 Aotu.vue

​		第三步:在index.js中注册

​		第四步在App.vue中使用

```js
 /**
   *    如何重定向呢
   *      path:'',
   *      redirect:'/home'    让他重定向为 home
   *
   *
   *     怎么改为history模式呢
   *     在inde.js中
   *      const router = new VueRouter({
             routes,
            mode:'history'
          })

```

App.vue

### l路由内的属性

​		 tag		让router-link 变成对应标签  tag="div"

​		active-class	在链接激活的时候使用的css类名

​		

​			

```js
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/home">Home</router-link> |
      <router-link to="/about"  >About</router-link>
      <router-link to="/aotu" tag="button">点我</router-link>
      <router-link  to="/sub" tag="div" class="dawo">打我</router-link>
      <button @click="handlesfa">爸爸</button>
      <button @click="handlesdawo">打我</button>
    </div>
    <router-view/>
  </div>
</template>
<script>
  /**
   *  在源码里有一个属性  this.$router
   */
  export default {
        name:'App',
        methods:{
          handlesfa(){
            // this.$router.push('/home');
            //如果不想操作返回
            this.$router.replace('/about')
            console.log('123')
          },
          handlesdawo(){
            this.$router.push('/aotu')
            console.log('打我')
          }

        }
      }
</script>




<style>
#app {
  -webkit-font-smoothing: antialiased;
}
  .dawo{
    width: 100px;
    height: 100px;
    background-color: red;
  }

</style>

```

### 路由的使用



### 如何拿到动态路由

​		   --->         $route.parmas.(你在index.js写的值)	例如     $route.parmas.zhangsan

## 路由懒加载

​		:什么是路由懒加载?

​			当打包构建应用的时候,javascript包会变的非常的大,影响页面加载.

​		 如果我们能把不同路由对应的组件分割成不同的代码块,然后当路由访问的时候才加载对应组件.这样就高效了

写法:	在index.js中配置路径的时候

```vue
compoent:()=>import()
```





## 嵌套式路由:

​	路由嵌套是一个很常见的功能

​		  比如在home的页面中,我们希望通过/home/news和/home/message来访问一些内容

​		 一个路径映射一个组件.访问这两个路径也会分别渲染两个组件

​	如何实现呢?

​		  1.创建对应的子组件.并且在路由映射里配置相应的子路由

​			 2.在组件内部使用

​		在index.js中

```js
 children:[
 {
        path:'',
        redirect:'messsge'
      },
 {
        path: 'news',
        name:'HomeNews',
        component: () => import('../views/HomeNews')
      },
 {
        path: 'messsge',
        name: 'HomeMessage',
        component:()=>import('../views/HomeMessage')
      }
 ]

```

在组件中:

​	2.在组件内部使用

```js

```
## 路由传递参数:

​	首先我们需要了解URL协议

​		scheme://host:port/path?query#fragment	也就是

​		 协议   ://主机  :端口/路径?查询

​	路由的传递由两种1

​		第一种:

​			 配置路由的格式     /xxx/:xxx    ---->动态路由

​			传递的方式:  在path后面跟上对应的值   :to="'/user/'+userid"

​			传递后形成的路径: /xxxx/xxx

​		第二种

​			 配置路由格式 /xxx 也就是普通配置

​			 传递方式:对象中使用query的key作为传递方式:

​				  :to="{path:'/profile',query:{name:'乾坤',age:'18'}}"		

​					这个query可以通过	**$route.query** 取出来

​					输出的结果: /profile?name=乾坤&age=18

​					传递后形成的路径:/xxx?xx=bb  xxx?xx=cc

​					

```js
//注册一个新路由
  {
    path:'/profile',
    name:'profile',
    component:()=>import('../views/Profile')
  }
//使用
   <router-link  :to="{path:'/profile',query:{name:'乾坤',age:'18'}}">我 的文件</router-link>
//怎么取出来呢 
	  <h2>{{$route.query}}</h2>		
```





## 传参进阶写法

```js
  <button @click="deif">我是传参1的另一个写法</button>
   <button @click="pirfile">我是传参2的另一个写法</button>


 deif(){
            this.$router.push('/user/'+this.userid)
          },
 pirfile(){
            this.$router.push({
              path:'/profile',
              query:{
                name:'qiankun',
                age:'18',
                tall:"180cm"
              }
            })
          }

```

## 全局守卫		写在index.js中

```js
//全局导航守卫		
/**
 *    前置钩子/守卫(回调) 在跳转之前就更改了
 *      
 *
 * */
router.beforeEach(function (to,form,next) {
  next()  //这个必须调一下 不然不会执行下一步
  document.title =to.matched[0].meta.title    //to就是上面定义的路由
  console.log(to)
  console.log('我先')
})
  //后置钩子
/** 在跳转之后回调
 *    如果是后置钩子 是不用next的
 * */
router.afterEach(()=>{
  console.log('我后')
})
```

## 生命周期使用1

```
*    生命周期函数:
*          created(){} 创建组件会回调的
*          mounted(){} 挂在到template会回调的
*          updata(){}  刷新页面会回调的.
*
```

## keep-alive让所有路径匹配的视图组件都被缓存 避免重新渲染

​		作用:让所有路径匹配的视图组件都被缓存 避免重新渲染

操作:

​		

```js
 再App中
 		         <keep-alive>
               	  <router-view></router-view>
                 </keep-alive>

          activated(当页面活跃的时候)  和  deactivated(当页面不活跃的时候)  是根keep-alive挂钩的
        这两个函数只有该组件被保存了使用了 keep-alive才是有效的
```

```
     我要是希望有的是频繁创建有的是不从新加载 那怎怎么办?   给组件一个name
       使用 exclude  属性任何匹配的组件都不会被缓存 传入字符串或者正则  切记 不要随便加空格
       使用include  只有匹配的数组会被缓存   
<keep-alive  exclude= '组件1name1,组件2name'>
 <router-view></router-view>
</keep-alive>
```

# Vuex

​	1.什么是vuex?

​			他是集中式存储管理应用的所有组件状态,并以相应的规则保证状态以一种可预测的方式发生改变

​	怎理解呢?

​		State:就是我们的状态(可以当作就是data中属性)

​		View:视图层.可以针对State的变化,显示不同的信息

​		Actions:这里的Actions主要是用户的各种操作:比如点击,输入都会导致状态变化



## Vuex状态管理

​		修改的时候 state----->Vue components---->Actions(这个是用来处理异步操作的.Mustations是不能处理异步的)------->Mutations     当然也可以跳过Actions这一步   浏览器可以通过Mustations(Devtools)来管理你到底哪个接面修改了哪些值 如果直接跳过这两部  从 Vue components到State来修改是不能监听到谁更改的



操作:

​		需要在store的index.js中写入

```js
export default new Vuex.Store({
  state: {
    counnter:1000     //变量
  },
  mutations: {        //写方法
    increment(state){
      state.counnter++;
    },
      decrment(state){
        state.counnter--;
      }

  },
```

怎么调用呢?

```js
//1.在#app中通过
$store.state.counnter

调用写的方法呢?
     methods:{
      adds(){
        this.$store.commit('increment')		//this.$store.commit('在index.js中定的方法名字')
      },
      subs(){
        this.$store.commit('decrment')
      }
```

## Vuex的核心概念

### State:

​	Vuex提出使用单一状态树

​	什么是单一状态树呢?

​			就是全部都使用一个state 不使用多个state

​	所以vuex也使用了单一状态树来管理应用层面的全部状态.这样可以让我们最直接的方式找到某个片段,而且在之后的维护和调试过程中,也可以非常方便的管理和维护



### Getters:

​	这个东西类似于计算属性

### Mutation

​	vuex的store状态更新的唯一方式:提交Mutation

​	mutation包括两部分

​	1.字符串的事件类型(type)

​	2.一个回调函数(handler),该回调函数的第一个参数就是state

### Action:

​	atction类似于mutation但是他是专门用来处理异步的比如网络请求

### Module:

​	module是模块的意思,为什么要在vuex中使用模块呢

​		vue使用单一状态树,也么也意味着很多状态都会交给vuex来管理

​		当应用变得非常复杂的时候,stote对象就会变得非常臃肿

​		为了解决这个问题,vuex允许我们将store分割成模块 (Module),而每个模块都拥有自己的state,

muation,action.getters等等

## getter花里胡哨的基础写法

```js
 state: {
    counnter:1000,     //变量
    students:[
      {id:100,name:'张三',age:18},
      {id:101,name:'李四',age:24},
      {id:102,name:'小白',age:25},
      {id:103,name:'乾坤',age:16},
      {id:104,name:'滚滚',age:30},

    ]
  },
getters:{
    powerCounter(state){
      return state.counnter*state.counnter
    },
    dayu(state){
    return state.students.filter(s=>s.age>20)
    },
    dayulength(state,getters){    //这个getters相当于最大的getters 通过这个拿到里面的方法
      return getters.dayu.length
    },
    moreaAgestudent(state){     //如果想让别人传参数可以这么搞	..很骚
        return function (age) {
          return state.students.filter(s=>s.age>age)
        }
    }
  }
//调用
    <h2>{{$store.getters.powerCounter}}</h2>
    <h2>{{$store.getters.dayu}}</h2>
    <h2>{{$store.getters.dayulength}}</h2>
    <h2>{{$store.getters.moreaAgestudent(25)}}</h2>

```

## Mutaion花里胡哨的基础写法			Payload

```js
//我想要在代码实现的时候.可以携带一些额外的参数
//比如 我想点击增加数字  我想增加一个名字 ,一串字符串 怎么做呢?
 <button @click="addfive(5)">+5</button>
    <button @click="addfive(-10)">+10</button>
    <button @click="addstudent()">添加学生</button>
      <h2>{{$store.state.students}}</h2>


 addfive(count){
        this.$store.commit('incrementaddfive',count)
      },
      addstudent(){
        let stu = {name:'乾坤',age:18,tall:'185cm'}
        this.$store.commit('addstudent',stu)
      }


//index代码
	 //这些称之为paylod :负载
    incrementaddfive(state,count){  //传入第二个参数 这个参数在App.vue里可以添加的形参传入过来
      state.counnter +=count
    },
    addstudent(state,student){
      state.students.push(student)
    }
```

## Mutaion的提交风格

​	他是包含一个type属性的对象:

​			如果用这种方法 那么他传入的他的值就是成为了对象了

```js
this.$store.commit({
  type:'incrementaddfive',
  count						//这个成对象了 如果传的比较多可以考虑这个写法
})
```

## Mutaion的响应规则

​	Vuex的store中的state是响应式的,当state中的数据发生改变的时候,Vue组件会自动更新

​	为什么是响应式呢??

​			**这些属性都会被加入到响应式系统中.而响应式系统会监听属性的变化.当属性的发生变化的时候,**

​	**会通知所有界面中用到该属性的地方.让界面发生刷新**



​	这就要求我们必须遵循一些vue对应的规则

​		提高在store中初始化好所需的属性

​			1.提前在store中初始化好所需要的属性

​			2.当给state中的对象添加新属性的使用 使用下面方式:

​				方式1:使用Vue.set(obj,newProp,123)

​				方式2:用新对象给就对象重新赋值

```js
 info:{
      name:'乾坤',
      age:18,
      tall:'200cm'
    }

  undateinfo(state,name){
        state.info.name = name;						//这个是新对老赋值
        // state.info['address'] = '洛杉矶'     //淦 为啥我的响应出来了
        Vue.set(state.info,'address','洛杉矶') //使用这个方法也可以
      delete  state.info.age;                 //该方式做不到响应式! 淦 为啥我又可以
        Vue.delete(state.info,'age')			//使用这个方法也可以
    }


 <h1>--------------------展示info的内容是不是响应式的</h1>
    <h2>{{$store.state.info}}</h2>
    <button @click="undainfo">点我便名字</button>
    <h2>{{$store.state.info}}</h2>
```

## Mutation类型常量

​	在使用  this.$store.commit('')		的时候 总是需要拷贝  那怎么办呢

````js
//第一步
	新建个js文件
		export  const  INCREMENT = 'increment'	
     
 //第二部
       在index.js中引用
			import {INCREMENT} from "./mutations-types";
		用的时候:
		 [INCREMENT](state){
     			 state.counnter++;
    			},
   //第三步 在app.vue中
            this.$store.commit(INCREMENT)

````

## Mutation同步函数

​	通常情况下vue要求我们Mutation中的方法必须是同步方法

​	主要的原因是当我们使用devtools的时候,可以devtools可以帮助我们捕获mutation的快照

​	但是如果是异步操作,那么devtools将不能很好的追踪这个操作什么时候会被完成.

​		虽然异步之后再页面中也显示出来了.但是 再devtoos里还是没跟踪上.

​			但是一定要有异步呢  ? 比如网络请求必定是异步操作 我们可以使用action

## Action花里胡哨的基础写法

```js
 actions: {
    aUpdata(content,payld){    //他的默认属性是context 理解为Store
      setTimeout(()=>{				//这里面执行异步操作
        content.commit('undateinfo')
        console.log(payld.message);
        payld.success();
      },2000)
    }
     
     //调用							通过dispatch 而不是通过commit
      this.$store.dispatch('aUpdata',{
          message:'我是携带的信息',
          success:()=>{
            console.log('里面完成了')
          }
        })
     /////再这里不一定使用content 也可以使用解构赋值
```

## Action进阶写法

```js
 aUpdata(content,payld){    //他的默认属性是context 理解为Store
      return new Promise((resolve,reject)=>{		//写一个Promise 再里面执行异步操作
        setTimeout(()=>{
          content.commit('undateinfo')
          console.log(payld);
          resolve('111')
        },1000)
      })
    }

//调用
   this.$store
              .dispatch('aUpdata','我是携带的信息')
              .then(res=>{							//这里执行返回成功的代码
                console.log('里面完成了提交')
                console.log(res)
              })
```

## Module的使用及其核心

首先可以再 根的module定义一个

​		比如    modules: {  a:modulea,},

然后使用它	他也是分为 5个核心

```js
const modulea = {
  state:{
    name:'张三',
    age:'18岁'
  },
  mutations:{
    updateName(state,paylod){
      state.name = paylod
    }
  },
  getters:{
    fullname(state){
      return state.name+'111'
    },
    fullname2(state,getters){
      return getters.fullname +'222'
    },
    fullname3(state,getters,rootstate){   //如果想获取根的值,方法 需要第三个参数
      return getters.fullname2+rootstate.counnter
    }
  },
  actions:{
    aupdatename(content){    //在这里的话 这个content就不能看作store了 他只会调用自己模块的mutations
      setTimeout(()=>{
          content.commit('updateName','王五')
      },1000)

    }
  }
}




 <h1>-------------------------APP中 modulea的内容</h1>
      <h2>{{$store.state.a.name}}</h2>
        <button @click="clearupname">修改名字</button>
        <h2>{{$store.getters.fullname}}</h2>
         <h2>{{$store.getters.fullname2}}</h2>
        <h2>{{$store.getters.fullname3}}</h2>
    <button @click="asynupdatename">异步修改名字</button>




 clearupname(){
        this.$store.commit('updateName','三少爷')
      },
      asynupdatename(){
        this.$store.dispatch('aupdatename')
      }

```

## Vuex的结构

​		不一定都写在index.js  他是可以抽离的

# 网络请求封装

​	vue中发送网络请求有非常多的方式,那么在开发中,如何选择呢?

	### 传统的Ajax是基于XMLHttpRequset(XHR)

​	那为什么不用他呢

​		非常好解释,配置和调用方式等非常混乱

​		编码起来看起来就非常蛋疼

### 所以真实开发中很少直接使用,而是使用jquery-Ajax

​	 相当于传统的Ajax非常好用

​	为什么不选择他呢

​		首先我们明确,在vue的整个开发过程中,都是不需要使用jquery

​		那么,就意味着为了方便我们经行一个网络请求,而特意引用jquer是不合理的

​	jquery的代码1w行

​	vue的代码也才1w行

完全没有必要为了用网络请求引用这个框架



## jsonp

​	在前端开发中,我们一种常见的网络请求方式就是jsonp



## axios

​	特点:
​			在浏览器中发送XMLHttpRequests亲求

​		在node.js中发送http请求

​		支持Promise API

​		拦截请求和响应

​		转换请求和响应数据

​		等等

axios(config)

axios.requset(config)

axios.get(url[config])

axios.delete(url[config])

axios.head(url[config])

axios.post(url[data[config]])

axios.put(url[data[config]])

axios.patch(url[data[config]])

## 基本使用

```js
axios({
  url:'http://123.207.32.32:8000/home/multidata',
  method:'get'        //如果写get就是get请求
}).then(res=>{
  console.log(res)
})

axios({
  url:'http://123.207.32.32:8000/home/multidata',
  //专门针对get请求的参数拼接
  params:{
    type:'pop',
    page:1
  }
}).then((res)=>{
  console.log(res)
})
axios({
  url:'https://jsonplaceholder.typicode.com/todos/'
}).then(res=>{
  console.log(res)
}).catch(err=>{
  console.log(err)
})
```

axios.all 处理并发

```js
axios.all([axios({
    url:'http://123.207.32.32:8000/home/multidata'
}),axios({
  url:'http://123.207.32.32:8000/home/multidata',
  params: {
    type:'sell',
    page:4
  }

})]).then(res=>{
      console.log(res)
    }).catch(err=>{
  console.log(err)
})
```

如何把两个并发的都拿出来呢

```js
axios.all([axios({
  url:'http://123.207.32.32:8000/home/multidata'
}),axios({
  url:'http://123.207.32.32:8000/home/multidata',
  params: {
    type:'sell',
    page:4
  }

})]).then(axios.spread((res1,res2)=>{
  console.log(res1)
  console.log(res2)
})).catch(err=>{
  console.log(err)
})
```

## 全局配置

```js
/**
 *    我们发现很多的BaseUrl是固定的
 *    事实上,在开发中可能很多参数都是固定的
 *    这个时候我们可以通过经行一些抽取,也可以利用axiox的全局配置
 *    就要用到 defaults了
 *
 *
 * */
axios.defaults.baseURL = 'http://123.207.32.32:8000'
axios.defaults.timeout = 5000
axios.all([axios({
  url:'/home/multidata'
}),axios({
  url:'/home/multidata',
  params: {
    type:'sell',
    page:4
  }

})]).then(axios.spread((res1,res2)=>{
  console.log(res1)
  console.log(res2)
})).catch(err=>{
  console.log(err)
})
```

## 常见的配置选项

### 	请求地址

​	url:'/user'

### 	请求类型

​	method:'get'

### 	请求根路径:

​	baseURL:

### 	请求前的数据处理

​	transformRequest:[function(data){}]

### 	请求后的数据处理

​	transfromResponse:[function(data){}]

### 	自定义请求头

​	header:{'x-Requseted-With':'XMLHttpRequest'}

### 	URL查询对象			(这个针对get请求的!!!!!)

​	params:{id:12}

### 	查询对象序列化函数

​	paramsSerializer:function(params){}

### 	request body			(post请求用这个!!!)

​	data:{key:'aa'}

### 	超时设置:

​	timeout:1000

### 	跨域是否带Token

​	withCreadentials:false

### 	自定义请求处理

​	adapter:function(resolve,reject,config){}

### 	身份验证

​	auth:{uname:'',pwd:'12'}

### 	响应数据的格式json/blob/document/arraubuffer/text/stream

​	responseType:'json'



## 在项目中我们一般不使用全局而是创建axios的实例		实例可以创建多个

```js
//创建对应的实例
  const  instance1 = axios.create({
  baseURL:'http://123.207.32.32:8000',
  timeout:5000,
})
instance1({
  url:'/home/multidata',
}).then(res=>{
  console.log(res)
})

```



## 避免代码耦合性 我们可以把网络请求封装在一起 还便于维护

```js
export function request(config) {
  return new Promise((resolve, reject) => {
    const  instance = axios.create({
      baseURL:'http://123.207.32.32:8000',
      timeout:5000
    })
      instance(config)
          .then(res=>{
            resolve(res)
          })
          .catch(err=>{
            reject(err)
          })
  })
}
//渐变写法
export function request(config) {

    const  instance = axios.create({
      baseURL:'http://123.207.32.32:8000',
      timeout:5000
    })
    return instance(config)
}

//调用
import {request} from "./network/request/request";
request({
  url:'/home/multidata'
}).then(res=>{
  console.log(res)
}).catch(err=>{
  console.log(err)
})
```



​	

## 拦截器			切记 拦截之后给人家return出来

//作用 如果获得到aaa中的一些信息不符合要求,把他拦截掉/

/2.比如我们每次发送网络请求的时候,都希望在页面显示一个i请求图标

//3.某些网络请求(比如登录),必须携带一些特殊的信息

```js
    instance.interceptors.request.use(aaa=>{     //request拦截请求
   
        console.log(aaa)
        return aaa
      },error => {
        console.log(error)
      })
    instance.interceptors.response.use(ccc=>{     //拦截响应
      console.log(ccc)
      //返回出去
        return ccc.data
    },error => {
      console.log(error)
    })      
```
# 总计大纲

​	1.  ref如果是绑定在组件中,那么通过**this.$ref.refname** 获取到的是一个组件对象

​	2.如果绑定的是绑定在普通元素中,那么通过this.$refs.refname获取到 是一个元素对象.

