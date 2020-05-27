# Vue Study Notes（Second Version）



## Day01-初识vue&事件绑定

​		**Vue** 是一套用户构建用户界面的<font color='red'>渐进式框架</font>，其核心库只关注视图层，易于上手，并且能和第三方库或者既有项目更好的整合。

​		**vue 和 react 的对比**：

|               区别               |                         Vue                         |                   React                    |
| :------------------------------: | :-------------------------------------------------: | :----------------------------------------: |
| 显示组件数据的方式（插值表达式） |                      {{数据}}                       |                   {数据}                   |
|        事件处理函数的判定        |                  等号左侧有vue指令                  |                等号右侧有{}                |
|          数据更新的方式          |             直接找到data中的值进行改变              |       使用setState之后触发render函数       |
|                                  |         单文件组件（内部直接添加style标签）         |    多文件组件（css文件和组件文件分开）     |
|             渲染方式             | Templates（即使vue也支持jsx，默认使用template模板） |                    JSX                     |
|      事件处理函数的传参方式      |   `@click='handleClick(数据1,数据2,...,$event)'`    | `onClick={(数据)=>this.handleClick(数据)}` |

​		**注：**在优化方面，对于 **React**，在应用中当某个组件的状态发生变化时，它会以该组件为根，重新渲染整个组件子树。如果要避免不必要的子组件的重渲染，需要使用 `PureComponent`，或者是手动实现`shouldComponentUpdate`方法。而使用`PureComponent`和`shouldComponentUpdate`时，需要保证该组件的整个子树的渲染输出都是由该组件的 **props** 所决定的。如果不符合这种情况，那么此类优化就会导致难以察觉的渲染结果不一致。

​		而在Vue应用中，组件的依赖是在渲染过程中自动追踪的，所以系统能精确知晓哪个组件确实需要被重渲染，相当于每个组件已经主动获得了`shouldComponentUpdate`，这样就不存在类似react中的问题了。

​		<font color='blue'>**Vue 对data数据的更改细节：**</font>

**对于对象：**

​		Vue 是无法感知对象的属性（property）的增加或者移除。由于Vue会在初始化实例时对property执行 `getter/setter`转化，所以property必须在 data对象上存在才能将它转换为响应式的

​		解决方法：使用 以下方法可以转为响应式的 porperty

```javascript
Vue.set(object,propertyName,value)
// 或者
this.$set(object,propertyName,value)
```

**对于数组：**

1. vue是不能感知数组对索引位的更改

2. vue可以感知数组的变异方法，即可以改变原数组（push，pop，shift，unshift，sort，reverse，splice，...）

   <font color='blue'>**Vue中的事件修饰符：**</font>

   ​		在原生js中，想要阻止事件传播或者阻止默认事件时很麻烦的，同样在react框架中也是如此，而为了解决这个问题，vue为 `v-on` 提供了专门的事件修饰符。

   - `.stop`			阻止事件传播，相当于 `e.stopPropagation()`

     ```html
     <div @click.stop='handleParent'>
         parent
         <div @click.stop='handleSon'>
             son
         </div>
     </div>
     ```

   - `.capture`      改事件处理函数在事件捕获阶段触发

   - `.prevent`       阻止默认行为，相当于 `e.preventDefault()` 

   - `.once`              事件处理函数只执行一次

     

     <font color='blue'>**Vue中的按键修饰符：**</font>

     ​	在监听键盘事件时，通常会根据键码值（keycode）来进行处理，而Vue为 v-on 提供了按键修饰符

   - `.enter`

     ```html
     <input type='text' @keyup.enter='handleInput' />
     ```

   - `.tab`

   - `.esc`

   - `.space`

   - `.up`

   - ...（详细可查看官网）

     当然，并不是所有修饰符都在上面，有些需要自定义按键修饰符，通过全局 `config.keyCodes` 来自定义

     ```JavaScript
     Vue.config.keyCodes.F5 = 116
     ```

     <font color='blue'>**Vue中的鼠标修饰符：**</font>

     ​	Vue还提供了鼠标修饰符	

   - `.right`

     ```html
     <div @mouse.right='handleMouse'></div>
     ```

   - `.middle`

   - `.left`



## Day02-基本指令

- **v-for**

  ​	`v-for` 是基于一个数组来渲染一个列表，使用 `item in items`形式的语法

  ```html
  <ul>
      <li v-for='(item,index) in arr' :key='item'>{{item}}</li>
  </ul>
  ```

  1. 数据为数组时，有两个变量（item，index）
  2.  数据为数字时，有两个变量（item，index）
  3. 数据为数字符串时，有两个变量（item，index）
  4. 数据为对象时，有三个参数（propertyValue，propertyName，index）
  5. 可以使用 of 代替 in 作为分隔符

  ​      <font color='blue'>注：使用 `v-for` 指令时最好为每一项提供一个 **key** 值，以便它能够跟踪每个节点的身份，从而重用和重新排序现有元素</font>

  ​	  <font color="red">详解 key 值：`key` 的特殊 attribute 主要用在 Vue 的虚拟dom算法，在新旧 nodes对比时辨识 VNodes。如果不使用 key 值，Vue会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。而使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。有相同父元素的子元素必须有**独特的** key。重复的 key会造成渲染错误。</font>

  

- **v-model**

  ​		`v-model` 在表单控件或者组件上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。

  ```html
  <div id='app'>
      <input type='text' v-model='msg' >
  </div>
  
  <script>
  	let vm = new Vue({
          el:'#app',
          data(){
              return {
                  msg:'Hello World'
              }
          }
      })
  </script>
  ```

  ​		<font color='blue'>在表单中，不同的表单控件收集到的数据也不同：</font>

  - 普通文本框/文本域			收集的是文本框的输入数据

  - 单选按钮                             收集的是单选按钮的 value 值

  - 单个复选框                         收集的是一个布尔值，选中为true，反之为false

  - 多个复选框                         收集的是一个数组，值为选中的复选框的 value 值

  - 下拉框                                 收集的是 option 的 value 值，若加上 multiple，则收集的是一个数组

    **修饰符**

  - `.number`                             处理数字格式的字符串，将其变为 Number 类型的数据

  - `.lazy`                                 数据变化后才响应，即不会执行 input 事件，而执行 change 事件

  - `.trim`                                  自动过滤掉输入字符首尾的空白符

    

<font color='red'>**重：Vue双向数据绑定原理**</font>

​	Vue.js 采用 **数据劫持** 结合 `发布者-订阅者` 模式的方式，通过 `Object.defineProperty()` 来劫持各个属性的 setter，gettter，在数据变动时发布消息给订阅者，触发相应的监听回调，从而进行数据响应。

```JavaScript
var obj  = {};
Object.defineProperty(obj, 'name', {
        get: function() {
            console.log('我被获取了')
            return val;
        },
        set: function (newVal) {
            console.log('我被设置了')
        }
})
obj.name = 'fei';//在给obj设置name属性的时候，触发了set这个方法
var val = obj.name;//在得到obj的name属性，会触发get方法
```

​	原理图：

![Two way data binding](https://images2017.cnblogs.com/blog/1162184/201709/1162184-20170918135341618-553576179.png)



## Day03-基本指令&计算属性

- **v-bind** （语法糖：`:xxx='aaa'`）

  ​	`v-bind`动态的绑定一个或者多个attribute，或一个组件prop到表达式。在绑定 `class` 或 `style` attribute 时，支持其它类型的值，如数组或对象。在绑定 prop 时，prop 必须在子组件中声明。

```html
    <div id="app">
        <h3 data-age=22>我是h3标题</h3>
        <h3 v-bind:zsp='a'>我是h3标题</h3>
        <h3 :zsp='a'>我是h3标题</h3>

        <!-- css行内样式 -->
        <div style="color: blueviolet;">css行内样式绑定</div>

        <!-- vue方式的样式绑定 -->
        <p :style='{backgroundColor:"skyblue",color:"red"}'>vue方式的样式绑定</p>
        <p :style='styleObj'>vue方式的样式绑定-将样式以对象形式分离出来</p>
        <p :style='styleArr'>vue方式的样式绑定-将样式以数组形式分离出来</p>

        <p :class='zsp'>单个类名绑定</p>
        <p :class='classArr'>多个类名以数组方式绑定</p>
        <p :class='classObj'>多个类名以对象方式绑定</p>
        <h2 :class='{red,blue}'>对象语法绑定属性，属性的值为布尔值</h2>
    </div>
```

<font color='blue'>注：没有参数时，可以绑定到一个包含键值对的对象。注意此时 `class` 和 `style` 绑定不支持数组和对象。</font>



- **v-if**

  ​	`v-if` 利用了原生 js 中对节点的 `create` 与  `remove` 方法来控制单个dom元素是否渲染在页面中，true表示渲染，false表示不渲染。如果要控制**多个dom元素**的显示，只需要在 `template` 标签中使用 **v-if** 指令。

  用法：

  ```html
  <!-- v-if 的值为表达式 -->
  <div v-if="Math.random() > 0.5">
    Now you see me
  </div>
  
  <!-- v-if 的值为变量 -->
  <div v-if='isShow'>
      xxxxx
  </div>
  ```

  

- **v-else**

  `v-else` 为 `v-if` 的 "else" 块

  <font color='blue'>注： v-else 必须紧跟在 v-if 或者 v-else-if 后面，否则不会被识别</font>

  

- **v-else-if**

  `v-else-if` 为 `v-if` 的 "else-if" 块

  <font color='blue'>注：v-else-if  必须紧跟在 v-if 或者 v-else-if 后面，否则不会被识别</font>

```html
<template v-if='loginType==="username"' >
   <label>用户名</label>
   <input placeholder='请输入用户名' key='1'>
</template>
<template v-else>
  	<label>密码</label>
    <input placeholder='请输入密码' key='2'>
</template>
<button @click='handleClick'>点击切换</button>
```

​		上述例子中 通过 v-if 和 v-else 指令来切换用户名输入框或密码输入框，Vue也尽可能高效的渲染元素，即会重复渲染 input 已有元素而非重新渲染，这样的话在用户名的input中输入的值切换时依然会存在于密码的input输入框内，而 Vue 使用 **key** 值来解决了这个问题，每个input具有单独的 key 值，从而在切换时区分二者。



- **v-show**

  ​	`v-show` 根据 css 的display 来控制dom元素是否渲染在页面中，true表示渲染，false表示不渲染。根据表达式值的真假来切换 dom 元素的 **display** 值（block/none）。

  ​	<font color='blue'>注：v-show 不支持 template 元素，也不支持 v-else。</font>

```html
 <h3 v-show='isShow'>我是三级标题</h3>
```



- **v-if  与 v-show 对比**

  ​	`v-if` 是”真正“的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。`v-if` 也是惰性的，如果在初始渲染时条件为假，则什么也不做，直到条件第一次变为真时，才会开始渲染条件块。

  ​	相比之下，`v-show` 就简单得多，不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS进行切换。

  ​	一般来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show` 较好，如果在运行时条件很少改变，则使用 `v-if` 较好。

  

- **v-if 和 v-for**

  当 `v-if` 和 `v-for` 一起使用时，v-for 的**优先级**会比 v-if 高，<font color='red'>**故不推荐同时使用 v-if 和 v-for**</font>

  下面看一个例子：

```html
<div id="app">
    <ul>
        <li v-for="(todo,index) in todos" v-if="todo.isComplate">
        	{{index}}
        </li>
    </ul>
    <ul>
        <li v-for="(todo,index) filterTodos">
        	{{index}}
        </li>
    </ul>
</div>

<script>
	let vm = new Vue({
        el:"#app",
        data(){
            return{
                todos:[
                    {isComplete:true}
                    {isComplete:false}
                    {isComplete:true}
                ]
            }
        },
        computed:{
            filterTodos(){	// 把todos中isComplete值为false 过滤掉，从而减少不必要的循环
        		return this.todos.filter(item=>item.isComplete)
    		}        
        }
    })
</script>
```

![v-if和v-for](https://github.com/heiye-vn/Vue-Notes/blob/master/images/v-if%E5%92%8Cv-for.png?raw=true)

​	上面例子中 循环 todos 列表，并且带有 v-if 条件语句时，因为 v-for 的优先级会比 v-if 高，所有通过渲染的 index 索引值可知 循环了三次，只是后面的 v-if 语句让一种一个未渲染，而使用 conputed 计算属性将 v-if 条件为假的条件块过滤掉，这样就减少了不必要的循环。解决了 v-if 和 v-for 同时使用带来的问题。



- **计算属性**

  ​	我们在处理逻辑时，一些简单的逻辑可以放在模板中，但是对于一些较为复杂的逻辑如果放在模板中，这样就会造成代码过于冗余，逻辑与视图高度耦合了。因此 Vue 提供了计算属性（**computed**）来专门处理一些逻辑。

```html
<div id='app'>
    {{number3}}
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data(){
            return{
                number1:10,
                number2:30
            }
        },
        computed:{
            number3(){
                return this.number1 + this.number2
            }
        }
    })
</script>
```

​		

- **计算属性（computed） 与 方法（methods）**

  ​	通过上述例子，我们可以看到，使用 `methods` 同样可也以实现。但二者是存在一定区别的。<font color='blue'>计算属性是基于它们的响应式依赖进行**缓存**的</font>。只在相关响应式依赖发生改变时它们才会重新求值。意味着只要 data 中的数据没有改变，多次访问时计算属性会立即返回之前的结果，不必要再次执行函数。相比之下，每当触发重新渲染时，调用方法（methods）将**总会**再次执行函数。

  ​	计算属性和方法的使用场景：需要做缓存时就使用 `computed` 计算属性，比如我们有一个性能开销比较大的计算属性A，他需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于A，如果没有缓存，将不可避免的多次执行 A 的 getter。当然，如果不希望有缓存，就可以使用 `methods` 方法来代替。



## Day04-基本指令&监听器

- **v-html**

  ​	`v-html` 用于将 字符串 html 转化成 html 标签，类似于原生js中的 `innerHTML`

  ```html
  <div id='#app'>
      <p v-html='msg'></p>
  </div>
  <script>
  	let vm = new Vue({
          el:'#app',
          data(){
              return{
                  msg:'<a href="#">我是a标签</a>'
              }
          }
      })
  </script>
  ```

  ​	Vue 中的  `v-html` 和 React 中的 `dangerouslySetInnerHTML` 都是将 字符串 html 解析成 真正的 html标签。



- **v-text**

  ​	`v-text` 用于更新元素的 contentText，一般使用插值符号 `{{}}` 来更新元素内容

  ```html
  <p v-text='msg'></p>
  ```

  

- **自定义指令**

  ​	在 Vue 中，除了系统内置的一些指令外，还可以允许用户注册自定义指令，而自定义指令又可以分为 `全局自定义指令` 和 `局部自定义指令`。

  ```html
  <div id='app'>
      <p v-color='color'>自定义指令</p>
      <input v-focus type='text'>
  </div>
  <script>
      // 注册全局自定义指令
      Vue.directive('focus',{
          bind(el,binding){
              // 聚焦元素
              el.focus()
          }
      })
      
  	let vm = new Vue({
          el:'#app',
          data(){
              return{
                  color:'hotpink'
              }
          },
          // 注册局部自定义指令
          directives:{
              color:{
                  bind(el,binding){
                      el.style.color = binding.value
                  }
              }
          }
      })
  </script>
  ```

  

- **监听器**

  ​	Vue通过 `watch` 选项来响应数据的变化，即监听数据变化。当需要在数据变化时执行异步或开销较大的操作时，使用该方式。

  ```html
  <div id='app'>
      <p>{{number}}</p>
      <button @click='handleClick'>点击更新数据</button>
  </div>
  <script>
  	let vm = new Vue({
          el:'#app',
          data(){
              return {
                  number:5,
                  arr:[1,2,3],
                      person:{
                          name:'zhangsan',
                          age:10
                      },
                      objctArr:[
                          {
                              name:'小明',
                              age:20
                          },
                          {
                              name:'小亮',
                              age:25
                          }
                      ]
              }
          },
          methods:{
              handleClick(){
                  // this.number++
                  
                  // this.arr[0]='张三'
                  // this.arr.push(9)
  
                   // this.person.name='张三'
                   // this.person.age=20
  
                   this.objctArr[1].name='小菲'
              }
          },
          watch:{		// 放置监听器
              number:{	// 配置number的监听器
                  handler(){	// number数据变化时触发
                      console.log('number数据变化了，已监听到')
                  }
              },
              arr:{    // 配置arr的侦听器
                      handler(){      // 当arr改变时触发
                          console.log('arr数据更新了，已监听到')
                      }
                  },
                  person:{    // 配置person的侦听器  会监听 person 中所有数据
                      handler(){      // 当person中任何一个数据改变时触发
                          console.log('person数据更新了，已监听到')
                      },
                      deep:true       // 监听对象属性的改变
                  },
                  'person.age':{    // 配置person的侦听器  会监听 person 中指定属性的变化
                      handler(){      // 当person中指定数据改变时触发
                          console.log('person数据更新了，已监听到')
                      },
                      deep:true
                  },
                  objctArr:{    // 配置objectArr的侦听器  
                      handler(){      // 当objectArr中数据改变时触发
                          console.log('objectArr数据更新了，已监听到')
                      },
                      deep:true
                  }
          }
      })
  </script>
  ```

  

- **计算属性（computed）和监听器（watch）**

  ​	在Vue中，可以通过一个计算属性和watch函数来监听某个数据属性的变化，但二者存在一定的差别。前面提到的，可以用计算属性实现的，就可以用方法（methods）实现。同样，可以用计算计算属性实现的，也可以用监听器（watch）实现，只要所依赖的相应数据不是频繁变化，开销不大的时候，就用计算属性，反之就用监听器。而且，计算属性不需要在 data 中进行定义变量，而监听器监听的变量需要在 data 中进行定义。



## Day05-过滤器&生命周期



































