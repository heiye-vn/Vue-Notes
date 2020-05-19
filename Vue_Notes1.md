# Vue Study Notes（Second Version）



### Day01-初识vue&事件绑定

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

   ​		在原生js中，想要阻止事件传播或者阻止默认事件时很麻烦的，同样在react框架中也是如此，而为了解决这个问题，vue为 v-on 提供了专门的事件修饰符。

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



### Day02



























