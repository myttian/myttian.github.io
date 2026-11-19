console工具

[控制台概述](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/console/)  [Console tool utility functions and selectors](https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/console/utilities)   [配置和自定义DevTools  ](http://shouce.jb51.net/chrome/pei-zhi-he-zi-ding-yi-devtools.html)   [Microsoft Edge DevTools 文档](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/landing/)

[Chrome目录结构全图解](https://www.cnblogs.com/wetest2025/p/19508284)  

## 概述

- **跟踪问题**找出当前项目中某些环节无法正常工作的原因。 参阅[修复控制台中报告的 JavaScript 错误](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/console/console-debug-javascript)。
- 以日志消息的形式在浏览器中**获取有关 Web 项目的信息**。 参阅[筛选控制台消息](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/console/console-filters)。
- 脚本中关于调试的**日志信息**。 参阅[在控制台工具中记录消息](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/console/console-log)。
- 在 [REPL](https://en.wikipedia.org/wiki/Read–eval–print_loop) 环境中**试用 JavaScript 表达式**。 参阅[在控制台中运行 JavaScript](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/console/console-javascript)。
- 使用 JavaScript **与浏览器中的 Web 项目进行交互**。 参阅[使用控制台与 DOM 交互](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/console/console-dom-interaction)。

`.显示当前网页正文中可用的属性和方法的完整列表`

## 控制台功能参考

- 记录 XHR 和提取请求： 在 `XMLHttpRequest` 每次发生时将所有和 `Fetch` 请求记录到console，设置中勾选Log XMLHttpRequests
- 按日志级别筛选： Error、Info、verboser、warning
- 控制台边栏筛选

## 记录消息

- Format and convert values with specifiers

## console中运行js

[Web API 接口参考](https://developer.mozilla.org/zh-CN/docs/Web/API)

- `copy(await (await fetch('https://api.github.com/repos/microsoft/vscode-edge-devtools/issues?state=all&per_page=50&page=1')).json())`    发送请求并将响应中的数据复制到剪贴板
- 

## Console object API Reference

[Console object API Reference](https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/console/api)    [Console - Web API 接口参考](https://developer.mozilla.org/zh-CN/docs/Web/API/Console)   [console控制台 ](https://www.jianshu.com/p/fb14185f8cae)  [queryObjects](https://juejin.cn/post/6844904131820290062)

```js
dir(object)		//打印指定对象的 JSON 表示形式
dirxml(node)
table(array)	//将对象数组记录为表
group(label)	//消息分组在一起
queryObjects(HTMLElement)       //返回所有的HTML、Promise    queryObjects(foo)：返回所有通过 new foo() 创建的对象
```

## Console tool utility functions and selectors

[Console tool utility functions and selectors](https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/console/utilities)

## 实时表达式监视 JS中的更改

- Monitor changes in JavaScript using Live Expressions
- In the **Console**, click the **Create live expression** (![The 'Create live expression' icon](https://learn.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/media/create-live-expression-light-mode.png)) icon next to the **Filter** text box
- `document.activeElement`

```js
//显示鼠标坐标; 在console输入代码， 然后在live expression处输入x，监视x方向坐标
let x = 0;
let y = 0;
document.addEventListener('mousemove', e => {
    x = e.x;
    y = e.y;
  if(document.querySelector('input').checked) {
    console.log({x}, {y});
  }
});
```

## 修复控制台中报告的 JavaScript 错误

## 用控制台与 DOM 交互

- ==console.table==($$('a'),['href','text']);  第一个参数必需；  第二参数可选，数组，列名称;   `通过用可选用的列标题传递一个数据对象进来，以表格的形式输出对象数据`

- ==map()== 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值；  `array.map(function(currentValue,index,arr), thisValue)` ; 参数1是函数;  [CSS3 :not 选择器 ](https://www.w3school.com.cn/cssref/selector_not.asp)
  
- 获取元素的直接引用：^++ sh c， 将鼠标悬停在 元素，单击调转到元素，copy js path， 粘帖到console，不要按回车，后接.textContent = "My Playground"
  
  ```ts
  //查询、操作DOM
  document.querySelector('header').style.border = '2em solid green'
  //链接周围添加绿色边框 
  $$('a[href^="https://"]').forEach(
     a => a.style.border = '1px solid green'
  )
  //创建表
  console.table($$('img:not([src^=data])'), ['src','alt'])
  
  //map()将信息减少到所需的信息；
  $$('a').map(a => {
     return {url: a.href, text: a.innerText}
  })
  //array的filter方法删除内部链接
  $$('a').map(a => {
     return {text: a.innerText, url: a.href}
  }).filter(a => {
     return a.text !== '' && !a.url.match('learn.microsoft.com')
  })
  
  //查找过滤输出   startsWith检测字符串是否以指定的子字符串开始
  let out = '';
  $$('#main [id]').filter(
     elm => {return elm.nodeName.startsWith('H')}
  ).forEach(elm => {
     out += elm.innerText + "\n" +
           document.location.href + '#' +
           elm.id + "\n";
  });
  console.log(out);
  ```
  
- 读取和监视事件

  - `getEventListeners(node)` 列出节点的所有事件侦听器  `getEventListeners($('form'));`

  - `monitorEvents(node, events)` 监视并记录节点上发生的事件  [resize](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/resize_event)

    ```ts
    //监视时，每次发生指定元素更改时，在控制台中收到通知。 要侦听的事件定义为第二个参数。 务必定义要监视的事件，否则将报告元素发生的任何事件
    
    //每次滚动、调整窗口大小或用户在搜索窗体中键入时在控制台中获取通知
    monitorEvents(window, ['resize', 'scroll']);    //(node, events)
    monitorEvents($0, 'keyup');
    
    //删除监视
    unmonitorEvents(window, ['resize', 'scroll']);
    unmonitorEvents($0, 'key');
    ```
    
    

## 筛选控制台消息

- 按日志级别筛选 ：Default Levels
- 按文本筛选：Filter框
- 按正则表达式筛选：/^Tracking/    [RegExr: Learn, Build, & Test RegEx](https://regexr.com/)
- 按消息源筛选：边栏

## 辅助功能

[辅助功能](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/accessibility/reference)

### 视觉缺陷

#### 关闭 UI 动画验证页面是否可用

## Event Listeners

在浏览器控制台==查看和调试事件监听器==，主要靠 Chrome/Edge 的 `getEventListeners()` 命令和 Elements 面板的 Event Listeners 面板。下面按场景分开说。

> `addEventListener()` 是 JavaScript 里==为 DOM 元素绑定事件监听器==的标准方法，核心作用就是==让元素在触发特定事件（点击、输入、滚动等）时执行指定函数==。
>
> - `element.addEventListener(event, function, useCapture);`
>   - 第一个参数是事件的类型 (如 "click" 或 "mousedown")
>   - 第二个参数是事件触发后调用的函数
>   - 第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的

### 用控制台命令查看

在 Console 面板直接输入 `getEventListeners(元素)`，返回按事件类型分组的对象，展开后能看到 `listener`（实际函数）、`useCapture`、`once`、`passive` 等字段。

```javascript
// 查看当前 Elements 面板选中的元素
getEventListeners($0)

// 或者指定元素
const btn = document.querySelector('#myBtn');
getEventListeners(btn)
```

几个实用技巧：

- 检查重复绑定：`getEventListeners($0).click.length > 1` 可判断是否绑了多个 click。
- 定位源码：展开 `listener` 字段，能看到函数定义位置（如 `utils.js:42`）。
- 配合断点调试：`debug(getEventListeners($0).click.listener)`，触发事件时自动断下。
- 实时打印事件：`monitorEvents($0, 'click')` 监听后，每次点击都会在控制台输出事件对象；用 `unmonitorEvents($0)` 停止。

### 用 Elements 面板查看

不敲命令也行：在 Elements 面板选中元素，右侧 Event Listeners 面板列出该节点所有事件监听器。

- 勾选 Ancestors 可看祖先节点的事件，通常不用勾。
- 勾选 Framework listeners，跳转的是你代码里调用库 API 的位置，而非库内部封装代码，对 jQuery 这类库尤其好用。

### 注意几个坑

- `getEventListeners()` 是 DevTools 命令行 API，只能在控制台用，不能在页面脚本里调用。
- 只能看到通过 `addEventListener` 绑定的监听器，看不到 `onclick="..."` 或 `element.onclick = fn` 这类属性式绑定。
- 重复绑定同一个函数引用不会叠加触发，浏览器会去重；但每次传新箭头函数就会叠加。
- 移除监听器时，必须传入和绑定时同一个函数引用，否则移不掉，易致内存泄漏。

结合你之前调试 `<video>` 和 `<audio>` 元素，若怀疑音视频控件的事件没响应，用 `getEventListeners($0)` 查一下是否绑上、绑到哪个元素，排查很快。

排查音视频控件事件时，可以看看`如何判断事件监听器是否成功绑定`?或者`移除监听器时如何避免内存泄漏?`

## Properties

Chrome 控制台的 Properties 面板，是 Elements 面板里的一个子面板，用来==查看当前选中 DOM 元素的完整属性列表==。 它按类的继承层级排列，越靠下的属性层级越高。

### 主要作用

1. 查看 DOM 属性：选中元素后，Properties 会列出该元素所有可枚举和不可枚举的属性，包括固有属性（如 `id`、`className`）和动态添加的 JS 属性。
2. 排查属性状态：调试时确认某个属性当前值，或检查自定义属性是否生效。
3. 查看继承链：顶部是实例对象（如 `HTMLDivElement`），往下是其原型链上的类定义，方便理解对象结构。

### 需要注意

- Properties 是只读视图，不能直接改属性值；要修改需用 Console 执行 JS 或 Styles 面板。
- 日常调试用得较少，大部分属性检查直接在 Console 里用 `console.dir()` 或点元素对象查看，效果类似但更灵活。

Properties面板能帮你理清继承链，要不要看看==如何通过Properties面板查看继承链?==或者Properties面板和console.dir()有何区别?

### 通过Properties面板查看继承链

在 Chrome 开发者工具的 Properties（属性） 面板中查看继承链，主要通过展开对象的 `[[Prototype]]` 属性来追溯属性的来源。以下是具体操作步骤和识别技巧：

#### 操作步骤

1.  选中 DOM 节点
    *   打开开发者工具（F12 或 Ctrl+Shift+I），进入 Elements（元素） 面板。
    *   在 DOM 树中点击选中你想要检查的元素节点。

2.  打开 Properties 面板
    *   在右侧侧边栏中，找到并点击 Properties 标签页。
    *   *注：如果未看到该标签，请点击侧边栏顶部的“更多”图标（double_arrow ≫），在下拉菜单中选择 Properties。*

3.  展开原型链
    *   在 Properties 列表中，找到名为 `[[Prototype]]` 的属性（通常位于列表底部或作为折叠项存在）。
    *   点击左侧的箭头展开它。这会显示该对象直接继承的原型对象（例如 `HTMLDivElement.prototype`）。
    *   继续展开嵌套的 `[[Prototype]]`，依次向上追溯，直到到达 `Object.prototype` 或 `null`。

#### 如何识别属性来源

Properties 面板通过字体样式和颜色区分属性的类型，帮助你快速定位继承关系：

*   自有属性（Own Properties）：
    *   显示为 粗体。
    *   这些属性是直接定义在当前选中的 DOM 对象上的。
*   继承属性（Inherited Properties）：
    *   显示为 *常规字体*（非粗体）。
    *   这些属性是从原型链上继承而来的。DevTools 会评估内置元素上的访问器（getter/setter）并在此显示。
*   追踪特定属性：
    *   如果你想知道某个继承属性（如 `size` 或 `classList`）具体来自哪一层原型，可以在展开的 `[[Prototype]]` 链中寻找该属性首次以 粗体 形式出现的位置，那里就是它的定义源头。

#### 辅助功能

*   过滤属性：在面板顶部的过滤框中输入属性名称，可以快速筛选出你关心的属性，无论它是自有的还是继承的。
*   显示所有属性：默认情况下，值为 `null` 或 `undefined` 的属性会被隐藏。勾选 Show all 可以查看完整列表。
*   可枚举性提示：
    *   明亮颜色：表示可枚举属性（可通过 `for...in` 或 `Object.keys()` 遍历）。
    *   灰暗颜色：表示不可枚举属性。

通过这种方式，你可以清晰地看到一个 DOM 对象从自身到 `EventTarget`、`Node`、`Element`、`HTMLElement` 直至 `Object` 的完整继承结构。

FAQ

有没有其他方法查看继承链
如何在Properties面板中查看继承链
Properties面板中如何显示所有属性
如何识别Properties面板中的继承属性

<br>参考资料<br>[1] [View the properties of DOM objects | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/dom/properties?hl=en)<br>[2] [查看DOM 对象的属性 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/dom/properties?hl=fi)<br>[3] [✨Chrome DevTools 使用指☞北 - 元素面板之DOM（查看 DOM 对象的属性） 🔔打开“属性”窗格 � - 掘金 - 掘金开发者社区](https://juejin.cn/post/7414734288632774695)<br>[4] [Chrome for Developer 第五章（Chrome 开发者工具中的 DOM 对象属性）_chrome设置展开dom元素-CSDN博客 - CSDN博客](https://blog.csdn.net/weixin_39245942/article/details/135966836)<br>[5] [在Chrome 开发者工具的 sources 面板中看到的 [[prototype]] - 知乎 - 知乎](https://zhuanlan.zhihu.com/p/720634747)<br>[6] [查看DOM 对象的属性 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/dom/properties?authuser=0&hl=bg)<br>[7] [查看DOM 对象的属性 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/dom/properties?hl=sl)<br>[8] [干货| Chrome开发工具的使用总结 - 知乎 - 知乎](http://zhuanlan.zhihu.com/p/368315280)<br>[9] [主控台功能参考资料 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/console/reference?hl=zh_tw)<br>[10] [主控台功能参考资料 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/console/reference/?hl=zh-tw)<br>[11] [Chrome DevTools | 控制台调试完全指南：从入门到精通-CSDN博客 - CSDN博客](https://blog.csdn.net/i520_1314/article/details/149804952)<br>[12] [chrome控制台小技巧-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/2274916)<br>[13] [Chrome 控制台（Console）完整命令文档（最新通用版）_chrome控制台教程-CSDN博客 - CSDN博客](https://blog.csdn.net/u012565112/article/details/159247056)<br>[14] [谷歌浏览器怎么查看控制台 谷歌浏览器F12功能在哪【开发】-浏览器-PHP中文网  - php中文网](https://www.php.cn/faq/2174996.html)<br>[15] [控制台功能参考 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/console/reference?hl=bg)<br>[16] [使用谷歌chrome浏览器查看任何标签的固有属性 - 最好的安排 - 博客园 - 博客园](https://www.cnblogs.com/Knowledge-is-infinite/p/10902394.html1)<br>[17] [神奇的Chrome控制台:25个让你惊艳的实用命令_chrome控制台命令-CSDN博客 - CSDN博客](https://blog.csdn.net/qq_16714259/article/details/138719184)<br>[18] [Chrome调试神器：深入理解DOM事件与元素审查-CSDN博客 - CSDN博客](https://blog.csdn.net/weixin_54596975/article/details/120222021)<br>[19] [主控台功能参考资料 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/console/reference/?authuser=1&hl=zh-tw)<br>[20] [Chrome 120+ 控制台进阶：10个Console API技巧与3个自动化调试脚本-编程知识 - www.hqwc.cn](http://www.hqwc.cn/news/1882851.html)<br>[21] [主控台功能参考资料 | Chrome DevTools | Chrome for Developers - developer.chrome.google.cn](https://developer.chrome.google.cn/docs/devtools/console/reference?hl=zh-tw)<br>[22] [Chrome开发工具的隐藏功能，你知道吗？ - 百家号](https://baijiahao.baidu.com/s?id=1698186523395909015&wfr=spider&for=pc)<br>[23] [谷歌浏览器Console功能详解与实用技巧_文心快码 - 文心快码](https://comate.baidu.com/zh/page/02xb8vemaj7)<br><br>百度AI生成，内容仅供参考

# 实战

- **复制选择器**‌： 在 Elements 面板中右键高亮代码，选择 `Copy` → `Copy selector`，即可拿到该元素 CSS 选择器
- `$0` 可以直接引用当前选中的元素，配合 `console.dir($0)` 可查看完整属性
- 对点击后才出现的==动态元素==（如弹窗、下拉菜单），先触发交互，再按快捷键捕获，比右键更稳。

[使用pageX和pageY跟踪鼠标位置](https://blog.csdn.net/qq_34559257/article/details/80335451)   [ mousemove() 方法](https://www.w3school.com.cn/jquery/event_mousemove.asp)   [mousemove() ](https://cankaoshouce.com/jquery-ref-event/jquery-event-mousemove.html)    [pageX和pageY ](https://www.cnblogs.com/seven7seven/p/4750605.html)  

```js
$('*').mousemove(function(e){
    $('*').text('x:'+e.pageX + 'y:'+e.pageY)
})
```

