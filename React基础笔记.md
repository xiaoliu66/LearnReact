# React基础笔记

## 1.hello_react

因为是刚开始学习React，没有用到React脚手架，所以要使用3个相关的js库。

* react.js：React核心库

* react-dom.js：提供操作DOM的react扩展库

* babel.min.js：解析jsx语法转为JS代码的库。

  

```html
<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>
    <!-- 引入react核心库 -->
    <script src="../js/react.development.js"></script>
    <!-- 引入react-dom,用于支持react操作dom -->
    <script src="../js/react-dom.development.js"></script>
    <!-- 引入babel,用于将jsx转为js -->
    <script src="../js/babel.min.js"></script>

    <script type="text/babel"> /*此处一定要写babel*/
        // 1.创建虚拟dom
        const VDOM = <h1>Hello,React</h1>
        // 2.渲染虚拟dom到页面
        ReactDOM.render(VDOM,document.getElementById('test'))
    </script>
</body>
```

## 2.虚拟DOM的两种创建方式

### 2.1 两种方式

1. 用jsx方式创建

   ```html
   <body>
       <!-- 准备好一个容器 -->
       <div id="test"></div>
       <!-- 引入react核心库 -->
       <script src="../js/react.development.js"></script>
       <!-- 引入react-dom,用于支持react操作dom -->
       <script src="../js/react-dom.development.js"></script>
       <!-- 引入babel,用于将jsx转为js -->
       <script src="../js/babel.min.js"></script>
   
       <script type="text/babel"> /*此处一定要写babel*/
       const VDOM = (
       	<h1 id="title">
       		<span>Hello,React</span>
           </h1>
       )
       ReactDOM.render(VDOM,document.getElementById('test'))
   ```

   

2. 用纯js方式创建（不推荐）

   ```html
   <body>
       <!-- 准备好一个容器 -->
       <div id="test"></div>
       <!-- 引入react核心库 -->
       <script src="../js/react.development.js"></script>
       <!-- 引入react-dom,用于支持react操作dom -->
       <script src="../js/react-dom.development.js"></script>
       
   
       <script type="text/javascript"> 
           // 1.创建虚拟dom
           const VDOM = React.createElement('h1',{'id':'title'},React.createElement('span',{},'hello,react')) /* 标签名称 标签属性 标签内容*/
           // 2.渲染虚拟dom到页面
           ReactDOM.render(VDOM,document.getElementById('test'))
       </script>
   </body>
   ```

### 2.2 虚拟DOM和真实DOM的比较

```html
<body>
        <!-- 准备好一个容器 -->
        <div id="test"></div>
        <!-- 引入react核心库 -->
        <script src="../js/react.development.js"></script>
        <!-- 引入react-dom,用于支持react操作dom -->
        <script src="../js/react-dom.development.js"></script>
        <!-- 引入babel,用于将jsx转为js -->
        <script src="../js/babel.min.js"></script>

        <script type="text/babel">
            /*此处一定要写babel*/
            // 1.创建虚拟dom
            const VDOM = (
                <h1 id="title">
                    <span>Hello,React</span>
                </h1>
            );
            // 2.渲染虚拟dom到页面
            const TDOM = document.getElementById("test")
            ReactDOM.render(VDOM, document.getElementById("test"));
            console.log("虚拟DOM",VDOM)
            console.log("真实DOM",TDOM)
        </script>
    </body>
```

<img src="D:\web\LearnReact\React基础笔记.assets\image-20210715204255463.png" alt="image-20210715204255463" style="zoom:80%;" />
关于虚拟DOM:

**1.本质是Object类型的对象**

**2.虚拟DOM比较‘轻’，真实DOM"比较重"**

**3.虚拟DOM最终会被React转化为真实DOM，呈现在页面上**

