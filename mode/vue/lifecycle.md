# 关于vue的第一篇

# Vue 是什么
Vue.js 是一套构建用户界面的渐进式框架。与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。
什么是渐进式框架,向上增量开发: 会在之后的文档中体现 【Vue 2.0，渐进式前端解决方案】


# Vue 解决了什么问题
Vue官网已经有很详细的一个说明，这里主要说明vue与react的一个区别
React 和 Vue 有许多相似之处，它们都有：
使用 Virtual DOM
提供了响应式 (Reactive) 和组件化 (Composable) 的视图组件。
将注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库


## 性能
React 和 Vue 在大部分常见场景下都能提供近似的性能。通常 Vue 会有少量优势，因为 Vue 的 Virtual DOM 实现相对更为轻量一些。如果你对数据感兴趣，可以参考这个专门测试渲染和更新性能的第三方跑分。注意这个跑分并不包含针对大量复杂组件树的情况，因此只建议作为参考。
优化

在 React 应用中，当某个组件的状态发生变化时，它会以该组件为根，重新渲染整个组件子树。
如要避免不必要的子组件的重渲染，你需要在所有可能的地方使用 PureComponent，或是手动实现 shouldComponentUpdate 方法。同时你可能会需要使用不可变的数据结构来使得你的组件更容易被优化。
然而，使用 PureComponent 和 shouldComponentUpdate 时，需要保证该组件的整个子树的渲染输出都是由该组件的 props 所决定的。如果不符合这个情况，那么此类优化就会导致难以察觉的渲染结果不一致。这使得 React 中的组件优化伴随着相当的心智负担。
在 Vue 应用中，组件的依赖是在渲染过程中自动追踪的，所以系统能精确知晓哪个组件确实需要被重渲染。你可以理解为每一个组件都已经自动获得了 shouldComponentUpdate，并且没有上述的子树问题限制。
Vue 的这个特点使得开发者不再需要考虑此类优化，从而能够更好地专注于应用本身。

## HTML & CSS
在 React 中，一切都是 JavaScript。不仅仅是 HTML 可以用 JSX 来表达，现在的潮流也越来越多地将 CSS 也纳入到 JavaScript 中来处理。这类方案有其优点，但也存在一些不是每个开发者都能接受的取舍。
Vue 的整体思想是拥抱经典的 Web 技术，并在其上进行扩展。我们下面会详细分析一下。

## JSX vs Templates
在 React 中，所有的组件的渲染功能都依靠 JSX。JSX 是使用 XML 语法编写 JavaScript 的一种语法糖。
JSX 说是手写的渲染函数有下面这些优势：
你可以使用完整的编程语言 JavaScript 功能来构建你的视图页面。比如你可以使用临时变量、JS 自带的流程控制、以及直接引用当前 JS 作用域中的值等等。
开发工具对 JSX 的支持相比于现有可用的其他 Vue 模板还是比较先进的 (比如，linting、类型检查、编辑器的自动完成)。
事实上 Vue 也提供了渲染函数，甚至支持 JSX。然而，我们默认推荐的还是模板。任何合乎规范的 HTML 都是合法的 Vue 模板，这也带来了一些特有的优势：
对于很多习惯了 HTML 的开发者来说，模板比起 JSX 读写起来更自然。这里当然有主观偏好的成分，但如果这种区别会导致开发效率的提升，那么它就有客观的价值存在。
基于 HTML 的模板使得将已有的应用逐步迁移到 Vue 更为容易。
这也使得设计师和新人开发者更容易理解和参与到项目中。
你甚至可以使用其他模板预处理器，比如 Pug 来书写 Vue 的模板。
有些开发者认为模板意味着需要学习额外的 DSL (Domain-Specific Language 领域特定语言) 才能进行开发——我们认为这种区别是比较肤浅的。首先，JSX 并不是免费的——它是基于 JS 之上的一套额外语法，因此也有它自己的学习成本。同时，正如同熟悉 JS 的人学习 JSX 会很容易一样，熟悉 HTML 的人学习 Vue 的模板语法也是很容易的。最后，DSL 的存在使得我们可以让开发者用更少的代码做更多的事，比如 v-on 的各种修饰符，在 JSX 中实现对应的功能会需要多得多的代码。
更抽象一点来看，我们可以把组件区分为两类：一类是偏视图表现的 (presentational)，一类则是偏逻辑的 (logical)。我们推荐在前者中使用模板，在后者中使用 JSX 或渲染函数。这两类组件的比例会根据应用类型的不同有所变化，但整体来说我们发现表现类的组件远远多于逻辑类组件。

## 组件作用域内的 CSS
除非你把组件分布在多个文件上 (例如 CSS Modules)，CSS 作用域在 React 中是通过 CSS-in-JS 的方案实现的 (比如 styled-components、glamorous 和 emotion)。这引入了一个新的面向组件的样式范例，它和普通的 CSS 撰写过程是有区别的。另外，虽然在构建时将 CSS 提取到一个单独的样式表是支持的，但 bundle 里通常还是需要一个运行时程序来让这些样式生效。当你能够利用 JavaScript 灵活处理样式的同时，也需要权衡 bundle 的尺寸和运行时的开销。
如果你是一个 CSS-in-JS 的爱好者，许多主流的 CSS-in-JS 库也都支持 Vue (比如 styled-components-vue 和 vue-emotion)。这里 React 和 Vue 主要的区别是，Vue 设置样式的默认方法是单文件组件里类似 style 的标签。
单文件组件让你可以在同一个文件里完全控制 CSS，将其作为组件代码的一部分。
<style scoped>
  @media (min-width: 250px) {
    .list-container:hover {
      background: orange;
    }
  }
</style>
这个可选 scoped 属性会自动添加一个唯一的属性 (比如 data-v-21e5b78) 为组件内 CSS 指定作用域，编译的时候 .list-container:hover 会被编译成类似 .list-container[data-v-21e5b78]:hover。
最后，Vue 的单文件组件里的样式设置是非常灵活的。通过 vue-loader，你可以使用任意预处理器、后处理器，甚至深度集成 CSS Modules——全部都在 <style> 标签内。
规模

## 向上扩展
Vue 和 React 都提供了强大的路由来应对大型应用。React 社区在状态管理方面非常有创新精神 (比如 Flux、Redux)，而这些状态管理模式甚至 Redux 本身也可以非常容易的集成在 Vue 应用中。实际上，Vue 更进一步地采用了这种模式 (Vuex)，更加深入集成 Vue 的状态管理解决方案 Vuex 相信能为你带来更好的开发体验。
两者另一个重要差异是，Vue 的路由库和状态管理库都是由官方维护支持且与核心库同步更新的。React 则是选择把这些问题交给社区维护，因此创建了一个更分散的生态系统。但相对的，React 的生态系统相比 Vue 更加繁荣。
最后，Vue 提供了Vue-cli 脚手架，能让你非常容易地构建项目，包含了 Webpack，Browserify，甚至 no build system。React 在这方面也提供了create-react-app，但是现在还存在一些局限性：
它不允许在项目生成时进行任何配置，而 Vue 支持 Yeoman-like 定制。
它只提供一个构建单页面应用的单一模板，而 Vue 提供了各种用途的模板。
它不能用用户自建的模板构建项目，而自建模板对企业环境下预先建立协议是特别有用的。
而要注意的是这些限制是故意设计的，这有它的优势。例如，如果你的项目需求非常简单，你就不需要自定义生成过程。你能把它作为一个依赖来更新。如果阅读更多关于不同的设计理念。

## 向下扩展
React 学习曲线陡峭，在你开始学 React 前，你需要知道 JSX 和 ES2015，因为许多示例用的是这些语法。你需要学习构建系统，虽然你在技术上可以用 Babel 来实时编译代码，但是这并不推荐用于生产环境。
就像 Vue 向上扩展好比 React 一样，Vue 向下扩展后就类似于 jQuery。你只要把如下标签放到页面就可以运行：
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
然后你就可以编写 Vue 代码并应用到生产中，你只要用 min 版 Vue 文件替换掉就不用担心其他的性能问题。
由于起步阶段不需学 JSX，ES2015 以及构建系统，所以开发者只需不到一天的时间阅读指南就可以建立简单的应用程序。

## 原生渲染
React Native 能使你用相同的组件模型编写有本地渲染能力的 APP (iOS 和 Android)。能同时跨多平台开发，对开发者是非常棒的。相应地，Vue 和 Weex 会进行官方合作，Weex 是阿里的跨平台用户界面开发框架，Weex 的 JavaScript 框架运行时用的就是 Vue。这意味着在 Weex 的帮助下，你使用 Vue 语法开发的组件不仅仅可以运行在浏览器端，还能被用于开发 iOS 和 Android 上的原生应用。
在现在，Weex 还在积极发展，成熟度也不能和 React Native 相抗衡。但是，Weex 的发展是由世界上最大的电子商务企业的需求在驱动，Vue 团队也会和 Weex 团队积极合作确保为开发者带来良好的开发体验。
另一个 Vue 的开发者们很快就会拥有的选项是 NativeScript，这是一个社区驱动的插件。

## MobX
Mobx 在 React 社区很流行，实际上在 Vue 也采用了几乎相同的反应系统。在有限程度上，React + Mobx 也可以被认为是更繁琐的 Vue，所以如果你习惯组合使用它们，那么选择 Vue 会更合理。


# Vue 如何使用

## 思维模式的转变，“数据驱动”；
首先，“数据驱动” 是一种编程范式(Programming Paradigm)，相似的有很多，详情可以参考这里：https://en.wikipedia.org/wiki...
如果只谈前端，那么问题就会简化很多，一般来说，会比较 “数据驱动” 与 “事件驱动”。数据驱动思想的出现一定程度上弥补了事件驱动的不足。

## 事件驱动

```
先说事件驱动，一个很典型的例子就是 jQuery。用 jQuery 开发的页面执行初期就像这样：
通过特定的选择器查找到需要操作的节点 -> 给节点添加相应的事件监听
```

响应用户操作，效果是这样：
```
用户执行某事件（点击，输入，后退等等） -> 调用 JavaScript 来修改节点
这种模式，对于业务需求简单的页面来说没什么问题。只是现在前端越来越复杂，光用这样的模式已经满足不了很多大型项目的需求。另一方面，找节点和修改节点这件事儿，效率本身就很低。
```
因此出现了数据驱动模式，我们就拿其中的一种，MVVM 来举例子，执行初期就像这样：

## 数据驱动模式
读取模板，同时获得数据，并建立 VM(view-model) 的抽象层 -> 在页面进行填充
要注意的是，MVVM 对应了三个层，M - Model，可以简单的理解为数据层；V - View，可以理解为视图，或者网页界面；VM - ViewModel，一个抽象层，简单来说可以认为是 V 层中抽象出的数据对象，并且可以与 V 和 M 双向互动（一般实现是基于双向绑定，双向绑定的处理方式在不同框架中不尽相同）。
针对用户的操作，大致是这样：

用户执行某个操作 -> 反馈到 VM 处理（可以导致 Model 变动） -> VM 层改变，通过绑定关系直接更新页面对应位置的数据
总结一下，可以简单的这么去理解：数据驱动不是操作节点的，而是通过虚拟的抽象数据层来直接更新页面。我觉得，主要就是因为这一点，数据驱动框架才得以有较快的运行速度（因为不需要去折腾节点），并且可以应用到大型项目。

总结： 我们的思维要做什么操作，不是关心如何查找到这个dom,并对dom进行操作，而是转变为我们如何定义数据，操作数据，再展示数据

# Vue环境搭建
  为了更加快速的上手项目，我建议使用`命令行工具 (CLI)`Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。该工具提供开箱即用的构建工具配置，带来现代化的前端开发流程。只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目：
  ```js
  // 全局安装 vue-cli
  npm install --global vue-cli
  //创建一个基于 webpack 模板的新项目
  $ vue init webpack my-project
  //安装依赖,走你
  $ cd my-project
  $ npm install
  $ npm run dev
  ```
  其他环境配置可参考官网

# 从我们的新的思维模式分的三步开始去了解Vue

  ## 1、定义数据，（定义数据模型）
  每个 Vue 应用都是通过 Vue 函数创建一个新的 Vue 实例开始的：
  ```js
    var vm = new Vue({
      // 选项
    })
  ```
  ### 1.1、使用data 定义数据
  选项中的data对象用来定义数据,定义count初始化值为0
  ```js
    var vm = new Vue({
      data: {
        count: 0
      }
    })
  ```
  组件的定义中只接受函数
  ```js
  data() {
    return {
      count: 0
    }
  }
  ```
  注： data中的定义的属性为响应式，何为响应式，如何实现响应式后面讲解。
  
  ### 1.2、使用props定义数据 
  可以是数组或对象，用于接收来自父组件的数据。props 可以是简单的数组，或者使用对象作为替代，对象允许配置高级选项，如类型检测、自定义校验和设置默认值。
  ```js
  var vm = new Vue({
      props: {
        count: 0
      }
    })
  ```

  ### 1.3 使用propsData定义数据
  ```js
  var Comp = Vue.extend({
    props: ['msg'],
    template: '<div>{{ msg }}</div>'
  })
  var vm = new Comp({
    propsData: {
      msg: 'hello'
    }
  })
  ```
  注： 只用于 new 创建的实例中，创建实例时传递 props。主要作用是方便测试。

  ### 1.4 使用computed定义数据
  相比data 他的作用： 计算属性： 计算属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算；
  场景： 用于数据的变化操作
  ```js
  data() {
    return {
      count: 0
    }
  },
  computed: {
    isShow: function() {
      return this.count > 0 ? true : false
    }
  }
  ```
  注意，不应该使用箭头函数来定义计算属性函数 (例如 isShow: () => this.count > 0)。理由是箭头函数绑定了父级作用域的上下文，所以 this 将不会按照期望指向 Vue 实例，this.count 将是 undefined。


  ## 2.展示数据
  Vue自定义的一套模板模板语法进行数据的展示
  
  ### 2.1“Mustache”语法
  
  #### 2.1.1文本输出
  采用 “Mustache”语法 (双大括号) 进行文本的输出
  ```js
  <span>总计：{{count}}<span>
  ```

  #### 2.1.2表达式
  大括号中支持js表达式
  ```js
  <span>{{ count > 0 ? true : false }}</span>
  ```

  ### 指令
  
  #### v-html
  ```js
  data() {
    return {
      rawHtml: '<p>1</p><p>2</p>'
    }
  },
  ...
  <span v-html="rawHtml"></span>
  ```
  ####  其他指令 v-if、v-for、

  ```js
   <span v-if="count">长度为：{{count}} </span>
  ```

  #### 指令参数
  一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，v-bind 指令可以用于响应式地更新 HTML 属性：
  ```html
  <a v-bind:href="url">...</a>
  ```

  ## 3.操作数据
  在什么时候操作数据？
  1、点击事件中去操作 ==》  method
  2、某些场景下去操作==》   生命周期



vue的学习成本相对较低，上手较快，但对于一个框架你没有使用到极致，无法去评判它的好与不好，先读懂它再使用它，再否定它；

# vue的生命周期

每个Vue实例被创建之前都要经过一系列的初始化过程，
 1. 数据观测模板（Observe data ）
    ```
    `如何实现数据的观测`
    ```
 2. 编译模板
    ```
    `(2)编译过程`
    ```
 3. 挂载实例到DOM
    ```
    `(3)哪些实现`，
    ```
 4. 然后数据更新时更新DOM
    ```
    `(4)如何实现`，
    ```
 在这个过程中，实例也会调用一些生命周期的钩子`在钩子中做一些自定义逻辑`


 # webpack结合Vue的脚手架和如何编译