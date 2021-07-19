# React基础笔记

## 1. React入门

### 1.1 hello_react

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

### 1.2 虚拟DOM的两种创建方式

#### 1.2.1 两种方式

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

#### 1.2.2 虚拟DOM和真实DOM的比较

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

### 1.3 jsx语法规则

jsx语法规则：

​            1.定义虚拟DOM时，不要写引号。

​            2.标签中混入JS表达式时要用{}。

​            3.样式的类名指定不要用class，要用className。

​            4.内联样式，要用style={{key:value}}的形式去写。

​            5.只有一个根标签

​            6.标签必须闭合

​            7.标签首字母

​                (1).若小写字母开头，则将该标签转为html中同名元素，若html中无该标签对应的同名元素，则报错。

​                (2).若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错。

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
            //1.创建虚拟DOM
		const VDOM = (
			<div>
				<h2 className="title" id={myId.toLowerCase()}>
					<span style={{color:'white',fontSize:'29px'}}>{myData.toLowerCase()}</span>
				</h2>
				<h2 className="title" id={myId.toUpperCase()}>
					<span style={{color:'white',fontSize:'29px'}}>{myData.toLowerCase()}</span>
				</h2>
				<input type="text"/>
			</div>
		)
		//2.渲染虚拟DOM到页面
		ReactDOM.render(VDOM,document.getElementById('test'))

		/* 
				jsx语法规则：
						1.定义虚拟DOM时，不要写引号。
						2.标签中混入JS表达式时要用{}。
						3.样式的类名指定不要用class，要用className。
						4.内联样式，要用style={{key:value}}的形式去写。
						5.只有一个根标签
						6.标签必须闭合
						7.标签首字母
								(1).若小写字母开头，则将该标签转为html中同名元素，若html中无该标签对应的同名元素，则报错。
								(2).若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错。

		 */
        </script>
    </body>
```

### 1.4 模块与组件、模块化与组件化的理解

#### 1.4.1 模块

1. 理解：向外提供特定功能的js程序, 一般就是一个js文件
2. 为什么要拆成模块：随着业务逻辑增加，代码越来越多且复杂。

3. 作用： 复用js, 简化js的编写, 提高js运行效率

#### 1.4.2 组件

1. 理解：用来实现局部功能效果的代码和资源的集合(html/css/js/image等等)

2. 为什么要用组件： 一个界面的功能更复杂

3. 作用：复用编码, 简化项目编码, 提高运行效率

#### 1.4.3 模块化

​	当应用的js都以模块来编写的，这个应用就是一个模块化的应用

#### 1.4.4 组件化

​	当应用是以多组件的方式实现, 这个应用就是一个组件化的应用

## 2. React面向组件编程

### 2.1 React中定义组件的两种方式

**1.函数式组件**

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
        // 1.创建函数式组件
        function Demo() {
            console.log(this) // 此处的this是undefined,因为babel编译后开启了严格模式。
            return <h2>我是用函数定义的组件（适用于【简单组件】的定义）</h2>
        }
        //2.渲染组件到页面
        ReactDOM.render(<Demo/>,document.getElementById('test'))
        /*
            上面的代码执行后，
            1.react解析组件标签，找到了Demo组件。
            2.发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM,随后呈现在页面中。
        */
    </script>

</body>
   ```

**2.类式组件**

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
        // 1.创建类式组件
        class MyComponent extends React.Component{
            // render是放在哪里的？-MyComponent的原型对象上，供实例使用。
            // render中的this是谁？-MyComponent的实例对象。
            render() {
                return <h2>我是用类定义的组件适用于【复杂组件】的定义</h2>
            }
        }
        //2.渲染组件到页面
        // 上面的render()和这里的render 没有任何
        ReactDOM.render(<MyComponent/>,document.getElementById('test'))
        /*
            上面的代码执行后，
            1.react解析组件标签，找到了Demo组件。
            2.发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM,随后呈现在页面中。
            3.将render返回的虚拟DOM转为真实DOM,随后呈现在页面中。
        */
    </script>

</body>
```

### 2.2 组件实例三大属性__state

1.完全写法

```html
<body>
	<!-- 准备好一个“容器” -->
	<div id="test"></div>
	
	<!-- 引入react核心库 -->
	<script type="text/javascript" src="../js/react.development.js"></script>
	<!-- 引入react-dom，用于支持react操作DOM -->
	<script type="text/javascript" src="../js/react-dom.development.js"></script>
	<!-- 引入babel，用于将jsx转为js -->
	<script type="text/javascript" src="../js/babel.min.js"></script>

	<script type="text/babel">
		//1.创建组件
		class Weather extends React.Component{
			
			//构造器调用几次？ ———— 1次
			constructor(props){
				console.log('constructor');
				super(props)
				//初始化状态
				this.state = {isHot:false,wind:'微风'}
				//解决changeWeather中this指向问题
				this.changeWeather = this.changeWeather.bind(this)
			}

			//render调用几次？ ———— 1+n次 1是初始化的那次 n是状态更新的次数
			render(){
				console.log('render');
				//读取状态
				const {isHot,wind} = this.state
				// 事件名称后面不要带括号，加了括号在页面渲染完后就会自动调用该方法。 React会在触发该事件之后自动调用该方法。
				return <h1 onClick={this.changeWeather}>今天天气很{isHot ? '炎热' : '凉爽'}，{wind}</h1>
			}

			//changeWeather调用几次？ ———— 点几次调几次
			changeWeather(){
				//changeWeather放在哪里？ ———— Weather的原型对象上，供实例使用
				//由于changeWeather是作为onClick的回调，所以不是通过实例调用的，是直接调用
				//类中的方法默认开启了局部的严格模式，所以changeWeather中的this为undefined
				
				console.log('changeWeather');
				//获取原来的isHot值
				const isHot = this.state.isHot
				//严重注意：状态必须通过setState进行更新,且更新是一种合并，不是替换。
				this.setState({isHot:!isHot})
				console.log(this);

				//严重注意：状态(state)不可直接更改，下面这行就是直接更改！！！
				//this.state.isHot = !isHot //这是错误的写法
			}
		}
		//2.渲染组件到页面
		ReactDOM.render(<Weather/>,document.getElementById('test'))
				
	</script>
</body>
```

