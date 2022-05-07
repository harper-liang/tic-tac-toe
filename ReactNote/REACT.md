>是什么
>1. 构建用户界面的JavaScript库
>2. 遵循组件设计模式、声明式编程范式和函数式编程概念
>3. 使用虚拟DOM来有效地操作DOM，遵循从高阶组件到低阶组件的单向数据流

>特性
>1. JSX语法
>2. 单向数据绑定
>3. 虚拟DOM
>4. 声明式编程
>5. Component

> 组件有两种数据：父组件传递的参数 Props和组件内部的状态State

> 数据驱动
> 界面都是根据数据来渲染，且随着数据变化，自动更新，这就是数据驱动渲染

#### 文档阅读-核心概念
> react应用程序组成部分：元素和组件
##### 1. JSX简介
  (1) 是什么？
  - JavaScript语法扩展。具有JavaScript的全部功能。
  - JS和XML结合的一种形式
  - 把HTML代码写在JS里，那就是JSX

  (2) 为什么
  - 将标记与逻辑共同存放在称之为“组件”的松散耦合单元之中，实现关注点分离。(是指按照功能分离》)

  (3) 嵌入表达式 { JavaScript 表达式 }

##### 2. 元素渲染
(1) 元素可以是DOM标签，也可以是用户自定义的组件
将一个元素渲染为DOM
```
ReactDOM.render(
  <h1>Hello</h1>
)
```
##### 3. 组件
接受props，返回用于描述页面展示内容的react元素
(1) 定义组件
  - 函数组件
  ```
  function myData(props) {
    return <h1>{this.props.name}</h1>
  }
  ```
  - ES6的class
  ```
  class myData extends React.Component {
    render() {
      return <h1>{this.props.name}</h1>
    }
  }
  ```
(2) 使用，直接写成标签形式即可
(3) ? 当 React 元素为用户自定义组件时，它会将 JSX 所接收的属性（attributes）以及子组件（children）转换为单个对象传递给组件，这个对象被称之为 “props”
##### 4. state和生命周期
  (1) state 
    - 允许 React 组件随用户操作、网络响应或者其他变化而动态更改输出内容。
    - 组件私有的。属于当前组件
    - 当需要state时，使用类形式定义组件(具体ES6语法)
    - 在class构造函数给state赋初始值
    - 通过super(props)将props传递到父类构造函数中
    - 修改State
      - 用setState({})
      - 异步更新setState((state, props)=>{})
  (2) 生命周期
    - 组件挂载 componentDidMount(),在组件已经被渲染到 DOM 中后运行
    - 组件卸载 componentWillUnmount()
  (3) 数据是向下流动的
#####  5. 事件处理
  (1) 显式阻止默认行为preventDefault()
  (2) 处理函数定义
  - render函数中直接使用箭头函数定义/bind绑定this
  - class fields语法，箭头函数作为属性值赋给类属性/bind绑定
  - 推荐：class fields语法

  (3) 向事件处理函数传递参数：箭头函数或bind方法
##### 6. 条件渲染
- 元素变量。变量存储元素。
-  && 与运算符:true则运行右侧，否则跳过
-  ? : 三目运算符
-  隐藏组件，条件控制，返回组件或null
##### 7. 列表 Key
##### 8. 表单
##### 9. 状态提升，共享变量放到父组件
##### 10. 组合和继承，一般组合就可以，props可以当作糙
  - 组件可以接受任意 props，包括基本数据类型，React 元素以及函数
##### 11. 思考如何构建一个应用
  - 分析设计稿：
     - 将UI划分为组件：将组件当作一个函数或对象，根据单一功能原则判定组件的范围(一个组件原则上只能负责一个功能)
     - 划分层级：包含，并列关系
  - 用React创建一个静态版本：将渲染UI和添加交互两个过程分开
     - state 代表了随时间会产生变化的数据，应当仅在实现交互时使用。
     - 目前只需提供 render() 方法用于渲染
     - 自下而上或自上而下构建
  - 确定UI的最小最完整的state
     - 找出引用需要的数据，看哪些是可以归纳到state中的。
     - 只保留应用所需的可变 state 的最小集合，其他数据均由它们计算产生。(保证state的小巧干练，没有多余的变量)
     - 通过问自己以下三个问题，你可以逐个检查相应数据是否属于 state：
      该数据是否是由父组件通过 props 传递而来的？如果是，那它应该不是 state。
      该数据是否随时间的推移而保持不变？如果是，那它应该也不是 state。
      你能否根据其他 state 或 props 计算出该数据的值？如果是，那它也不是 state。
  - 确定state的位置：共享数据的组件或更高层级组件中
  - 添加反向数据流：回调函数将调用 setState()更新应用

######  组件分为这几个部分： 构造函数constructor()、生命周期、渲染函数render()
######  执行顺序：ReactDOM.render()、组件的constructor()、render()、生命周期