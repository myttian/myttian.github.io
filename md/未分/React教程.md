## React教程

视频： [React全家桶移动端猿题库项目实战](https://www.bilibili.com/video/BV1uq4y1q7NM/?vd_source=7346303e5e18677d7261c2c0c109ecfd)   

[React中文官网](https://react.docschina.org/)

JSX语法、组件传值、生命周期函数、路由原理、React路由、状态管理ReactRedux、类组件、函数式组件、常用ReactHooks、高阶组件

[2023比较流行的九大前端框架](https://www.genban.org/teach/teach-39166.html)  [菜鸟教程](https://www.runoob.com/react/react-tutorial.html)   [Babel原理及其使用](https://www.jianshu.com/p/e9b94b2d52e2) [Babel-js编译器](https://blog.csdn.net/weixin_45143481/article/details/111491299) [react三大属性之refs ](https://www.cnblogs.com/virgosnail/p/15631086.html) [HTML中6种空白空格](https://blog.csdn.net/snans/article/details/129269665)  [React三大属性-模块化组件化区别](https://www.cnblogs.com/wyq1995/p/14792036.html)

[状态机](https://blog.csdn.net/m0_61703043/article/details/125853828)  [ 什么是状态机](https://blog.csdn.net/pingxiaozhao/article/details/109239311)

```
模块化：就是将一个大的js文件按照一定的规则拆成很多小的js文件，形成一个个模块
组件化：就是将一个html页面拆分成一个个小的部分，每个部分可以进行复用，每一个部分都可以说是一个组件，可想而知，组件是包含了html，css样式和js
 
模块化只是针对js，而组件化是针对页面，包含了html，css和js
 
React组件里包含：state每个组件特有的数据、页面绑定的事件、生命周期钩子函数、render()渲染到页面上的元素等
```

```react
import React, { Component } from 'react'

export default class Son extends Component {
    state = {name:''}                                      //每个组件特有的数据   
    clickMe=() => {console.log('点击按钮')}                 //页面绑定的事件
    componentDidMount(){console.log('页面加载完成')}        //生命周期钩子函数
    render(){return(                                       //渲染到页面上的元素
        <div>
            <button onClick={this.clickMe}>点击我</button>
        </div>
    )}
}
```

- **组件的拆分**	[React三大属性](https://www.cnblogs.com/wyq1995/p/14792036.html)   [属性](https://www.cnblogs.com/panghexin/p/11469495.html)  [属性](https://www.jianshu.com/p/88dfbdd835f0)
  - 组件嵌套：父子组件，	组件并列：兄弟组件
- 组件之间通信：父子和兄弟组件分别是怎么传递数据
- 组件中的状态：就是每个组件中保存的数据
- **react中操作dom节点**：react是一个js库，有自己独特的操作dom节点的方式，就是ref
- 三大属性：state用于保存每个组件特有的信息，props用于组件之间的通信，ref是react提供的一种操作dom的方式

### React特点

1. **声明式设计**
2. **使用JSX语法**
3. **灵活**
4. **使用虚拟DOM、高效**
5. **组件化开发**
6. **单向数据流**

### 脚手架

[React简介](https://www.ngui.cc/article/show-960833.html?action=onClick) [create-react-app入门](https://www.jianshu.com/p/77bf3944b0f4/)  [ react快速开始](https://blog.csdn.net/inthat/article/details/121394510) [react框架的使用与配置](https://www.codenong.com/cs106406859/)  [NVM-版本管理](https://www.bilibili.com/read/cv16108420)  [ React技术点入坑](https://blog.csdn.net/Charlotte_99/article/details/128097773)

React推荐npx create-react-app创建React项目，npx

```ts
创建react项目：npx create-react-app rdemo
cd rdemo
code . 		//打开vscode
npm start	//运行项目
```



### day1

类/函数式组件、组件内部数据定义和获取、事件类型3种写法格式、双向数据绑定、数组渲染修改、父传子、子传父(接收父组件传过来数据时定义期望类型、定义默认值)

### day2

使用context进行props属性值的多级传递、**React生命周期**、不受控组件和受控组件、**路由**