# 前端面试题汇总
- cookie 的使用

- koa中间件实现原理

- 描述快速排序的实现

- 原型链相关问题

- react 生命周期

- react 性能优化

- vue 双向绑定原理

- 如何用 js 实现动画

- css 动画以及与 js 动画性能比较

- 二叉树

- 二叉树后序排序

- 模板引擎实现原理

- 介绍实习经历，项目经验

  怎么做同构以及同构的两份代码的差异性

  koa中间件执行顺序以及如何实现

  跨域问题

  jsonp 的原理以及优缺点

  vue双向绑定原理

  jquery 和 vue 性能比较以及使用场景

  什么是高阶组件

  假设我维护一个服务端渲染框架，如何不侵入用户代码的情况下通知用户代码错误点（同时也要保证页面正常渲染）（这道题应当是开放题，答得不好）

  未来三年职业规划

  js bridge 原理（因为我第一家实习公司是做 ionic 混合开发，所以他问了这道题。很尴尬，我是真的答不出。面试官很惊讶，说：“你难道不专注原理吗？”）

  https 和 http 的不同之处

  http 2.0 的特性

  如何实现一个promise

  用 nodejs 做过什么

  graghQL 和 RESTful Api

  ### typeof实现的原理是什么？

  ### js继承是如何实现的？原理是什么？

  解释了一下js的原型链，但感觉表达的不够清楚。发现心里明白是一回事，说明白又是另一回事啊

  ### 给一个function A一个function B，A中有属性手写实现B继承A。并做到尽可能优化的继承实现

  当时准备写一下寄生组合式的继承方式，不过手写过程中貌似写错不少内容，手写代码能力还是要提高。寄生组合式继承实现：

  ```
  function inheritPrototype(SuperType, SubType) {
      var prototype = Object.create(SuperType.prototype);
      prototype.constructor = SubType;
      SubType.prototype = prototype;
  }

  function SuperType(props) {
      this.props = props;
  }

  function SubType(props) {
      SuperType.call(this, props);
  }

  inheritPrototype(SuperType, SubType);

  ```

  具体到A和B即A为SuperType，B为SubType。
  另附`Object.create()`的实现，在传入一个参数时`Object.create()`和下面的`object()`行为相同。(`Object.create()`可选传入第二个参数，其中可以定义新对象的额外属性，如`Object.create(SuperType, {name: {value: 'Test'}}`)

  ```
  function object(obj) {
      function F() {};
      F.prototype = obj;
      return new F();
  }

  ```

  ### 一个简单的算法题：求一个数组中第K大的数字

  ### 手写原生ajax请求

  1. 写完后面试官在`if (xhr.readyState == 4 && xhr.status == 200)`的地方又提了很多状态码的问题，比如此处的status换成201可不可以
  2. 因为我直接写了`var xhr = new XMLHttpRequest()`，没有提供IE的兼容，面试官又问了IE兼容的问题。

  比较完备的答案：

  ```
  function createXHR() {
      if (window.XMLHttpRequest) {
          return new XMLHttpRequest();
      } else {
          // 兼容IE5和IE6
          return new ActiveXObject('Microsoft.XMLHttp');
      }
  }

  var xhr = createXHR();
  xhr.onReadyStateChange = function() {
      if (xhr.readyState == 4) {
      // 状态码为200至300之间或304都表示这一请求已经成功
          if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
              console.log(xhr.responseText)
          } else {
              ...
          }
      }
  }
  // GET
  xhr.open('GET', url);
  xhr.send();

  // POST
  xhr.open('POST', url);
  xhr.send(data);

  ```

  ### 之后是面试官画了一个草图，要求用html和css进行实现，内容涉及到左侧固定右侧自适应、垂直居中等内容。草图大概是这样：

  ![img](https://user-gold-cdn.xitu.io/2018/4/22/162ecd8aac5f8e77?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

  ### 平时写代码的时候如何进行错误处理?

  ### 对react和虚拟DOM有了解吗?

  ## 二轮面试

  ### 对html语义化有什么了解吗？有那些语义化的新标签？

  当时就答了一些语义化的标签。总结一下：
  语义化标签即标签本身的内容就能表示这个元素的意义给浏览者或者开发者。比如`<div>`和`<span>`就是没有语义的元素。而`<form>`表示一个表单或者`<table>`表示表格就是语义化的标签。
  H5中提供了很多新的语义元素，比如：

  - `<header> <nav> <aside> <footer>`几个标签用来表示页面的头部、导航和侧边栏等不同部分。
  - `<article>`元素表示文档、页面、应用或网站中的独立结构，其意在成为可独立分配的或可复用的结构，如在发布中，它可能是论坛帖子、杂志或新闻文章、博客、用户提交的评论、交互式组件，或者其他独立的内容项目。
  - `<section>`包含了一组内容及其标题。
  - `<figure>`规定独立的流内容如图像图表照片代码等，`<figcaption>`定义`<figure>`的标题。

  ### 看过哪些Bootstrap源码，Bootstrap有什么特性？

  这里就说了一下Bootstrap栅格化系统的大概实现，说了一下Bootstrap的响应式。然后面试官又顺带问了Bootstrap如何实现的响应式，我说使用了css的@media。然后他又问我还有没有什么其他的特性当时没想起来

  ### 对flex了解有多少？flex有哪些基本的属性？

  就答了一下基本的`justify-content`和`align-items` `flex-direction`等等

  ### 如何实现两列等高布局？

  在问的过程中还问了`height: 100%`相关的问题

  ### 如何清除浮动？

  这里就打了使用`clear: both`，面试官说还有什么别的方法吗，说只有`clear: both`还不够，没有答上来

  ### css中单位`em`和`rem`有什么区别？

  - `rem`是相对于根的`em`，rem即root的em，相对于html根元素
  - `em`是相对长度单位，相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。事实上，根据W3标准，em单位是相对于使用em单位的元素的字体大小。父元素的字体大小可以影响em值是因为继承。
  - 总结：`rem`单位翻译为像素值是由html元素的字体大小决定的。此字体大小会被浏览器中字体大小的设置影响，除非显式重写一个具体单位。`em`单位转为像素值，取决于他们使用的字体大小。 此字体大小受从父元素继承过来的字体大小，除非显式重写与一个具体单位。

  `这部分内容转自: https://www.w3cplus.com/css/when-to-use-em-vs-rem.html © w3cplus.com`

  ### 如何将文字超出容器的部分变成省略号（...）

  ### 手写一个倒计时页面

  1. 这里因为我用了`var date = new Date()`，所以面试官就又问了这个date的时间是什么时间？是当前时区的事件还是电脑的时间还是什么别的？这个没答上
  2. 因为我本身用的`setInterval()`去实现倒计时，里面写的是1000毫秒执行一次，所以面试官就又问了一下js任务队列的内容，问我是不是浏览器能保证1000毫秒执行一次。我说由于任务队列的关系主线程不一定能保证1000毫秒执行一次，他又问我有什么优化方式吗？我说可以使用`requestAnimationFrame`进行循环调用，这样浏览器自身会进行优化，面试官又问我浏览器是怎么优化的(真是一问到底)，这里就答不上来了。

  ### 如何判断一个变量是不是数组？

  ### js中instanceof是如何实现的？

  ### 使用过ES6哪些新特性，js的基本数据类型是哪些？ES6中有新的数据类型吗？

  我就答了箭头函数、Map、Set等，面试官问了箭头函数的特点。ES6中多了Symbol这个新的原始数据类型，以前没怎么使用过，没有答上来。然后在提到Promise的时候问了Promise的问题：

  ### Promise是如何实现的？能不能自己写一个函数实现Promise？

  以前没有写过，就大概自己写了一个函数，结果面试官提出了我写的代码的各种问题，总之就是写的基本是错的。。

  ### http和https的区别？https的特点？

  ### 最常问的：从输入url到网页呈现的过程

  这里问到了发送http请求和DNS查询的顺序先后问题。

  ### DOM树和渲染树的加载先后？html、css、js的加载顺序是什么？(大概是这么问的)

  这里除了加载顺序还深入的问了比如DOM树是完全加载完毕在进行css的渲染吗？还是一边进行DOM树的构建一边进行css的渲染？如果html中有一段js代码进行很长时间的循环会不会影响页面的呈现？

