# webpack 总结

## 环境

1. nodejs 检查 cmd -> node -v
2. npm 检查 cmd -> npm -v  
   npm i webpack@4.41.6 -g 全局
   npm i webpack@4.41.6 -d 局部
3. yarn 检查 cmd -> yarn -v

## npm 和 yarn 常用命令

1. 安装命令
   npm install packName//install 缩写 i
   yarn add packName
2. 启动命令
   npm run serve(命令)
   yarn serve(命令)
3. 初始化环境
   npm init -y(当名称中无中文时)
   npm init(当名称中有中文时)
4. 根据 package.json 还原
   node_modules
   npm i
   yarn
5. npm config set registry https://registry.npm.taobao.org导入淘宝资源


## 定义

webpack 定义:
定义:前端自动化开发工具,打包器

## 作用

作用:所有的资源(html.css.js.img.font...)对 webpack 来说都是模块,打包的含义就是指对这些资源[模块]的编译,比如图片压缩,代码压缩等

## 功能

功能:编译 es6,打包字体,编译 css,压缩图片,代码热更新快速开发等

## 组成部分

mode:模式有两种 development(开发模式) production(生产模式)
entry:入口
output:出口
module:模块-->loader
plugins(普来个隐私):插件
devServer:开启本地服务,代码热更新

## 工作流程

当 npm 执行命令的时候:

1. 先读取 webpack.config.js
2. 执行 entry 指定的入口文件
3. 把所有入口文件里的资源通过 loader 和 plugins 处理解析
4. 把打包后的文件通过 output 存到指定的目录
   实例：webpack ./src/index.js -o ./build/built.js --mode=development

## loader 的执行过程

自下而上,从右向左执行

## loader 和 plugins 的区别

loader 用于解析处理资源
plugins 用于配置和加工资源或其他事项.一般来讲插件在 loader 执行完后执行

## 报错总结
1. TypeError: this.getOptions is not a function
   版本过高导致，或者版本不符
   解决办法：更换版本重试
2. 报错mode  mode: 'development'  //development为开发者环境，production为生产环境变量 ，还有一个为none
   解决办法：查看webpack.config.js文件所在位置是否正确或者mode值是否正确
# vue 环境

## npm run serve

开发环境 devDependencies

npm i -D name

## npm run build

生产环境 dependencies

npm or yarn
npm i name //安装到了生产环境里
npm i --save-dev name //生产环境的依赖包 (简写 npm i -S name //-S 可以不写)

全局环境
npm i -g @vue/cli

## 项目启动执行过程

当我们在 cmd 中输入`npm run xxx`的时候,脚手架 webpack 会执行第一个文件:src/main.js

main.js 又叫入口文件

根据 main.js 里引入的 vue 文件使用 vue-loader 去解析,以及 vue 文件中的图片,样式等使用的 loader 解析处理

## 脚手架与 vue 与 webpack 的关系

vue/cli 是脚手架,是作者基于 webpack 封装的

webpack 与 vue 没有关系,打包工具

vue 特指 vue.js 他是项目里运行的核心框架

## 项目创建

vue ui 使用图形化安装项目
vue create 项目名称 例 vue123 使用命令创建

## 项目结构

- dist 打包后的文件目录
- node-modules 项目运行时候的依赖
- public 公共目录,里面存放模板
- src 源代码目录
- package.json 非常重要
- README.md 项目说明文档
- .gitignore 过滤 git 仓库的工具
- babel.config.js 配置解析 es6 的

## vue 底层原理

Object.defineproperty()封装的
底饭破绕破题

## vue 是什么

以数据驱动视图的渐进式 mvvm 框架
简称响应式框架
m:数据 js 部分 v 视图 template 部分

## sass 语法

.scss 文件

- 安装:yarn add -D sass
  yarn add -D sass sass-loader@8.0.2
- 优点
  像写 js 一样去写 css 代码,有嵌套,变量等功能
  最终它会编译成原始的 css 代码

## cnd 方式引入 vue 和脚手架区别

脚手架是集成环境,使用 webpack 执行,而 cnd 方式使用原始的标签书写脚手架里的项目,全局中能有一个`new Vue`实例

### data 为什么是函数？
所有的子组件最终都要挂载到根实例上，
data 也会被合并掉，如果都是对象的话容易出现冲突等问题。函数写法的好处是，只有当该组件被加载的时候才会调用 data 函数，使用唯一的一个 data 数据，就不会出现该问题
例
{
name:123,
name:456
}

## spa 应用和单页面应用

- spa 应用就是单页面应用的另一种称呼
- 定义:vue 项目全局自由一个 html 文件,在项目的 public 目录里
- .vue 文件最后被编译成了 js 文件

## 单文件开发

# vue 指令

- v-text
  渲染文本内容的指令
  等价于插值`{{}}`,可渲染的值类型:数字,字符串,布尔,数组,对象
  可执行的表达式有:三元运算,四则运算,逻辑运算,自执行函数
  底层封装:innerText

- v-html 可以防止注入攻击
  渲染字符串类型的 dom 片段
  v-text 可以做的,他都可以.
  底层封装:innerHTML;

- v-model
  vue 响应式指令
  数据双向绑定指令,专门用于表单元素.

- v-once
  一次性渲染指令,永远只显示第一次的初始值 节省性能可以使用 v-once 让局部的标签缓存起来,不受更新的影响

- v-if
  条件渲染指令,他是控制元素销毁与渲染的

- v-show
  条件渲染指令,他是控制元素的 css 样式 display 属性,让元素显示与隐藏的

- v-bind
  动态绑定属性的指令
  缩写:`:` 英文的冒号
  绑定 class 和 style 有两种语法
  数组:`['active',{key:true}]`
  对象`{title:true,other:true}`
  动态绑定属性名
  v-bind:[name]='value'
  可以动态的控制属性名
  修饰符:.prop `v-bind:mysrc.prop='http://xx'`
  mysrc 属性怎不会渲染到页面中,防止代码被偷窃

- v-for
  循环渲染,列表渲染
  基础语法:
  `<p v-for="(item,index) in data" :key="index">{{item}}</p>`
  [重点]
  使用 v-for 必须加 key,且 key 的值必须唯一不可重复
  可渲染值类型:number,string,array,object

  为什莫要加 key?
  因为使用 v-for 循环渲染出来的虚拟 dom,他们是不固定的,如果不加 key,当其中一个的数据发生了修改,diff 是不知道具体修改的是谁.所以给每一个遍历出来的元素加一个身份标识,便于 diff 去操作.
  如果没有 key,则直接用新的 dom 替换旧的 dom,性能开销很大.所以 key 也是用于优化性能的

  什么是虚拟 dom?
  通过 js 算法生成出来的是虚拟 dom,在 vue 里叫 vnode,是通过 diff 算法计算得出的

  什么是 diff 算法?
  新旧 dom 同层对比,发现不一致的 dom 时,直接用新 dom 替换旧 dom,所以 diff 算法非常快

- v-on: 事件绑定指令
  缩写:`@`
  语法: `<button @click='fn'><button/>`
  如果事件直接给一个函数名则该函数会自动注入一个 event 对象
  传参:`<div @click='fn(123,$event)'>txt<div/>`
  显示传参的时候,如需使用 event 则需要手动传入`$event`
  event 对象的重要属性:
  event.target 事件触发元素 事件源
  event. currentTarget 事件绑定的元素
  事件修饰符
  .stop 阻止冒泡事件
  .prevent 阻止默认事件
  .once 绑定一次性事件
  .native 绑定原生事件
- v-slot 插槽值令
  只能用于 template 标签上.
  匿名插槽使用 default 做名称:`v-slot:default`

  定义:插槽是摸具,插入一定内容输出一定内容.
  多用于 ui 组件的开发

  v-slot 的缩写是`#`

  具名插槽:v-slot:name
  在模板组件中`<slot name='xx'></slot>`

  插槽传参:父传子还是在模板组件上使用自定义属性传参.
  子传父的时候,子组件在 slot 标签上使用属性传参.父组件在插槽的 template 标签上接收
  `<template #name='data>{{data}}</template>`

  p{我是首页}===>`<p>我是首页</p>`

# 样式和组件

## 样式作用域

在组件的 style 标签上写 scoped 属性,当前组建的所有标签上加一个哈希值,样式自动使用属性选择器,保持了样式的唯一不会污染全局

## 组件模块化开发

1. 必须首写字母大写
2. 使用模块化语法引入到父组件中
3. 父组件中使用 components 挂载

## 什么是模块化开发

稿可复用重复的代码块

## 路径缩写符`@`

`@`它是`src`文件夹目录的地址缩写,表示绝对路径

插入模块
export default{
components
:{
Home:require('./Home.vue).default
}
}

# 生命周期

## 生命周期是什麽?

页面从初始化到完成渲染,经过更新后销毁的过程

## 定义

组件的创建,挂载,更新,销毁四大阶段构成了组件的生命周期

## 组成部分

### 创建阶段

- beforeCreate 创建前 初始化组件,这时候 data 和函数等还没又被解析
- created 创建后 解析 data 和函数等,一般这里做骨架屏用

### 挂载阶段

- beforeMount 挂载前 把数据 data,函数和观测等与虚拟 dom 解析绑定和处理.这个时候还没有挂载到页面上
- mounted 挂载后 [重要] 页面上已经显示内容了,一般在这里进行 ajax 自动请求数据

### 更新阶段

- beforeUpdate 更新前 当 data 数据更新的时候,该函数还可以对数据进行二次修改
- updated 更新后 只能用于观测 data 更新的值

### 销毁阶段 [次重要]

- beforeDestroy 比 for 底四到瑞 销毁前
- destroyed 销毁后 用于清除常驻内存的垃圾,比如定时器

axios // 用 promise+ajax 封装的,好处是解决了回调地狱的问题,还可以在 nodejs 服务中运行
jsonp

# 属性 props

## 定义

vue 中的 props 指的是父组件向子组件传数据

## props 特点

数据流是单向的,是自上而下的,并且 props 只能使用,不能修改

## 语法

1. 父组件:`<Child></Child>`
2. 子组件:

```js
{
  props: ['list'] //or object
}
```

## 注意

1. 组件不能修改 props
2. props 的数据会自动提升到 this 对象上,它会和 data,methods 一样都会把属性名提升到 this 上,所以,命名的时候千万不能重复

## 分支管理

### 主分支

master 意味这正式发布的代码

### 开发分支

leader-dev 小组组长分支
songyu001-dev 我的分支
other00x-dev 别人的分支

songyu001-dev 开发，开发完，先把代码本地，然后从远程 master 拉最新的代码下来，再把自己的本地代码上传到远程的自己的开发分支 songyu001-dev，登陆远程账户，发起一个合并请求，请求把自己的分支 songyu001-dev 合并到 master。

1. 创建分支
   git branch name
2. 切换分支
   git checkout name
3. 创建并切换
   git checkout -b name
4. 合并分支
   git merge name master
   特别注意:【切换的时候一定要先把当前分支的代码存储到本地】
   如果是新建的文件,需要使用的 git add 和 git commit
   如果是修改了文件,则 git commit -am 'name'

# 组件通信

## v-on 和 emit

子传父，父组件用 v-on 给子组件绑定一个方法，子组件用`$emit`调用

## v-bind 和 props

父传子，父组件用 v-bind 给子组件传递数据，子组件用 props 来接受

## ref【非常不推荐使用】

父组件用 ref 来获取子组件的实例对象，然后就可以操作子组件的数据等

## children【不推荐】

父组件获取所有子组件的实例对象

## parent【不推荐】

子组件获取父组件的实例对象

## root

获取根实例，也就是 new Vue 实例对象

## v-model

会向自定义组件注入一个 value 属性和一个 input 函数
value 属性用 props 获取，input 方法用`$emit`调用

## .sync【推荐使用】

他是属性修饰符，可以让属性拥有伪双向绑定特性。在子组件中必须使用特定语法修改
`<child v-bid:msg.sync='msg'><child/>`
子组件
`this.$emit(update:msg,'新值')`
【使用场景】
关闭子组件里的弹出框的时候。

## bus

中央时间池，他不是 api，最早的 vue1.0 时代，由程序员们自己通过`$on和$emit`组合实现的一种非官方的组件通信方式

## attrs 和 listeners【推荐】

跨层级的，attrs 把数据传递给所有的后代组件，listeners 把方法传递给所有的后代组件

## vuex【处理中大型项目】

全局状态管理器

# 数据监听和计算属性

## watch 数据监听

定义:它用来对一个数据进行监听,比如 data.props 等.

### 监听的几种语法

1.简单数据类型的值:数字,字符串,布尔
`value(newVal,oldVal){}` 2.引用数据类型的值:数组和对象

#### 对象的点语法

该用法只用于监听对象里的某一个属性值的变化
`"obj.key"(newKey,oldKey){}`

#### 深度监听[数组或对象]

```js
watch:{
  arr:{
    handler(newArr,oldArr){},
    //开启深度监听
    deep:true
  }
}
```

#### 默认执行一次监听动作

```js
watch:{
  obj:{
    handler(newObj,oldObj){},
    deep:true,
    immediate:true
  }
}
```

### watch 的优势

1. 他专门用于监听一个数据
2. 他可以执行异步代码[非常重要]

### watch 的缺点

1. 他对数组和对象监听不友好,需要使用额外的语法去支持

## computed 计算属性

它和 watch 功能类似,都是可以对一个数据进行监听.
定义:不同的是它监听一个值,返回一个新值.

### 优点

1. 有缓存,当被监听的数据发生了改变,他会用上一次旧数据和本地新数据做对比,如果不一致才会执行,如果一致则不执行
2. 不收数据类型的影响

### 缺点

不能执行异步代码,他是一个同步的,数据响应后它必须立即做出反应

### 基础使用

```js
computed:{
  newStr(){
    return this.str+1
  }
}
```

### 修改

```js
computed:{
  newStr(){
    get(){},
    set(){}
  }
}
```

# 内置组件

## 定义

凡是纯小写的标签,他既不属于原生 html 标签也不是自定义组件,那么他就是 vue 内置的组件,所以叫内置组件

## template

模板组件,即是 vue 组件的包裹容器,也用于插槽使用

## slot

插槽的接收组件

## component

动态加载组件,该组件必须使用 is 属性,且 is 属性必须接收的是 data 里的值.根据 is 属性的组件名称来动态的加载组件.其执行的表现形式与 v-if 一样

## keep-alive

缓存组件,默认该组件里被包裹的所有组件都被缓存到内存中,即便是被 v-if 销毁的组件也同样会缓存

- include 只缓存 include 里面的组件,其他的不缓存
- exclude 除了 exclude 里面的组件不缓存,其余都缓存
  所以,include 和 exclude 中能二选一
  include 和 exclude 接收的值类型:

1. 数组
2. `a,b`
3. 'home'
4. /a|b/

## transition

# 自定义系列

## 自定义

### filter 过滤器

在 vue1.0 时代,内置了很多现成的过滤器,比起大小写转换,给数字加单位或取小数位

vue2.0 就只生一个过滤器了

#### 全局过滤器

`Vue.filter('name',()=>value+'11')`

#### 组件过滤器

```
filters:{
  name(value){
    return value.toString()
  }
  ...
}
```

### 过滤器的使用方式

`{{value | filter}}`
多个过滤器一直用管道符隔开

### 过滤器传参

可以接收额外的参数
`{{ value | filter(2)}}`

### 定义

在不修改原始数据情况下,对数据进行处理,并返回新值

### 使用场景

购物车里的数字加钱的单位,给数字取小数位

## directive 自定义指令

### 定义

使用 directive 创建的指令叫做自定义指令,用于扩展 vue 指令里没有的功能,比如让 input 框自动获取焦点

### 组件内自定义指令

directives,可以创建很多个指令.语法如下:

```js
directives:{
  focus:{
    inserted(el,binding,vnode,oldnode){
      el.focus()
    }
  }
}
```

#### 指令生命周期里参数解读

- el:指令绑定的元素
- binding:元素的属性,其中 value 是指令赋予的值
- vnode:当前最新的虚拟 dom
- oldnode:旧的虚拟 dom

### 指令里的钩子函数

- bind:第一次指令函数绑定时候执行,用于初始化数据
- inserted:相当于 mounted,用于处理 dom
- update:当组件更新的时候,操作
- componentUpdate:当自己和所有子元素都更新完毕后执行
- unbind:接触指令和元素的绑定

# 递归组件

无限级折叠菜单,树形菜单等

## 条件

1. 递归组件自身必须要有 name 属性,且 name 属性的值必须是当前组件名称
2. 递归组件的初始数据,必须来自于上游组件传递
3. 必须要有判断条件,用于终止递归调用

## v-if 和 v-for 一起使用谁先执行?

先走 v-if 后走 v-for,官方说过尽量这两个命令不要一起使用,太消耗性能

# 插件开发和混入

## 混入 mixins

它的作用是为了给组件瘦身,把组件中固定不变的代码抽离出来作成一个 js 文件,然后在引入组件中,使用 mixins 挂载,mixins 是一个数组写法

### 执行的机制

- 覆盖策略:data 和 methods 里的数据方法名字如果和混入里的重复,则会用组件里的替换掉混入里的.
- 合并策略:data 和 methods 里的名称,如果组件和混入不一样则合并在一起
- 生命周期:如果混入和组件有相同的生命周期,先执行混入里的,再执行组件里的

### 插件开发

1. 插件必须是一个对象
2. 对象里必须使用 install 的函数开发插件
3. 插件必须使用 Vue.use()安装

### 执行逻辑

当插件被 Vue.use 方法安装的时候,use 方法会自动的向插件的 install 函数注入一个 Vue 函数

我们使用这个 Vue 构造函数可以开发全局组件,全区指令,全局过滤器等

### 插件的配置

当使用 Vue.use 安装插件的时候,可以额外的传入一个对象,该对象就是默认配置项
