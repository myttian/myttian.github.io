[使用“元素”工具检查、编辑和调试 HTML 和 CSS ](https://learn.microsoft.com/zh-cn/microsoft-edge/devtools-guide-chromium/elements-tool/elements-tool)

元素工具检查、编辑和调试 HTML 和 CSS

## Accessibility

[无障碍](https://cloud.tencent.com/developer/article/1726231)  [Accessibility ](https://learn.microsoft.com/zh-tw/archive/microsoft-edge/legacy/developer/devtools-guide/elements/accessibility)  [Accessibility ](https://www.jianshu.com/p/07a6a2c6cd6f)让残疾人更好地使用网站；  

- 查看元素的位置 (可访问性树/无障碍树是 DOM 树的子集）。只包含来自 DOM 树的元素，这些元素可以展示在屏幕阅读器中页面的内容。

## 与DOM断点交互-DOM Breakpoints  

- `Elements`(元素)和`Sources`(源文件)面板中包含了用于管理DOM断点的窗格。每个断点都列出了一个元素标识符和断点类型
- 当触发一个DOM断点，断点在`DOM Breakpoints`(DOM断点)窗格中突出显示。`Call Stack`(堆栈)窗格显示调试器暂停的原因

## 查看元素事件监听器-Event Listeners

- 查看与DOM节点相关联的JavaScript事件

- 点击事件类型旁边的箭头（例如`click`）,可以看到已注册的事件处理程序的列表。 每个处理程序由类似CSS选择器的元素标识符标识，例如`document`或`button#call-to-action`。如果同一个元素注册了多个处理程序，元素会被重复列出。

- 事件处理程序的属性： handler包含一个回调函数。右键单击该函数并选择Show Function Definition(显示函数定义)以查看函数被定义在哪里（如果源代码可用） 。 useCapture一个布尔值，说明是否在addEventListener上设置了useCapture标志

- 祖先事件监听器： 勾选`Ancestors`复选框，除了当前选中节点的事件侦听器,还会显示当前选中节点的祖先元素的事件侦听器 。 取消勾选时，仅显示当前选定节点的事件侦听器

- 框架监听器

  ```
  一些JavaScript框架和库将原生DOM事件封装到自定义事件API中。在过去，这使得很难用DevTools检查事件侦听器，因为函数定义只是引用框架或库代码。Framework listeners(框架侦听器)功能解决了这个问题。
  
  当勾选Framework listeners(框架侦听器)复选框时，DevTools自动解析框架或库封装事件的代码，然后告诉你，代码中实际绑定事件的位置。
  
  当取消勾选Framework listeners(框架侦听器)复选框时，事件侦听器代码可能会解析框架或库代码中的某处
  ```

## Properties 面板

[Elements 面板](https://cloud.tencent.com/developer/article/1726231)

显示当前对象的所有属性：`dir(document.querySelector("body > h1"))`

## CSS功能参考

### 查看定义规则的外部样式表

- 单击 CSS 规则旁边的链接，打开定义规则的外部样式表
- Element_styles
  - 筛选元素的 CSS：color, **“样式”** 面板经过筛选，仅显示包含搜索查询 `color`的规则

### 仅查看实际应用于元素的 CSS-computed

- Element_computed
  - “ 样式” 面板显示应用于元素的所有规则，包括已重写的声明。 如果对重写声明不感兴趣，使用 “计算 ”面板仅查看实际应用于元素的 CSS。
  - **全部显示** ：显示所有继承的值

### 使用“Coverage覆盖”工具查看已用和未使用的 CSS

^++sh p运行show coverage；    [ JS 调试笔记](https://blog.csdn.net/jx520/article/details/105022869)

- 看下你写的那么多东西，到底那些地方都跑到了。修改多次的代码，难免产生废物，想清理一下么？
- 加载的每个文件中使用了多少 CSS (和 JavaScript) 。 绿色表示使用的 CSS。 红色表示未使用的 CSS
- 若要逐行显示所用 CSS 的明细，单击 CSS 文件； 红色行未使用

### 元素添加 CSS 声明的两种方法

- 添加内联声明(样式)； 在 element.style{}中添加
- 向现有样式规则添加 CSS 声明;  在要添加声明的样式规则的括号之间添加

### 元素添加类

.cls 

### 添加新样式

单击加号

- 选择要添加规则的样式表： 添加样式时，默认添加到inspector-stylesheet； 按住加号选择可选要添加到哪个样式表
- 样式规则添加到特定位置： 将鼠标悬停在样式规则上，insert style rule below

## 查看和更改css

### 查看元素的 CSS

### 向元素添加 CSS 声明

### 将 CSS 类添加到元素

### 向类添加伪状态

### 更改元素的尺寸

## 检查 CSS 网格

[传统模型、Flex和Grid布局](https://www.jianshu.com/p/33eaf65d80f8)

## styles中编辑css字体

字体编辑器要在实验中启用； 

## CSS-in-JS

使用 JavaScript 管理 CSS 代码；  用 JavaScript 定义 CSS 内容，最终 CSS 输出由应用实时生成

## 查看和更改 DOM

- edit as html ; ^+enter应用并关闭html编辑器
- **强制状态**：强制节点保持状态，包括 `:active`、、`:hover``:focus`、 `:visited`和 `:focus-within`
- console访问节点：==$0==当前选中节点 ； 
- **存储为全局变量**：如果需要多次引用某节点；右键；temp1为变量名
- 复制 JS 路径：自动测试中引用 JavaScript 路径； 右键copy>copy js path
- **中断dom更改**：js修改dom时暂停页面js 
  - 中断属性修改：中断导致节点属性发生更改的js
  - 中断节点删除：删除特定节点时暂停
  - 中断子树修改：添加或删除节点的任何后代时，将暂停

# Elements

## computed styles

“Computed Styles Sidebar”通常指浏览器开发者工具（DevTools）里 Elements 面板右侧的“Computed”样式侧栏，用于==查看选中元素经过层叠、继承和单位解析后的最终 CSS 值==。

### 核心用途

1. 查看最终生效值：不关心写了多少条重叠规则，直接显示浏览器实际用于渲染的最终值，如 `font-size: 70%` 会显示为 `14px`。
2. 定位样式来源：展开属性旁的箭头，能看到是哪条 CSS 规则最终生效，点击链接可直接跳转到源码位置。
3. 检查盒模型：顶部有可视化盒模型图，展示 `margin`、`border`、`padding`、`content` 的实际尺寸，方便排查溢出或对齐问题。

### 与 Styles 面板的区别

- Styles：规则视图，按层叠顺序列出所有命中的声明，显示来源和是否被覆盖（删除线），可实时编辑调试。
- Computed：结果视图，只展示最终采纳的值，所有缩写属性会展开为长属性（如 `margin: 10px` 拆成四边具体值）。

### 使用建议

排查样式问题时，先用 Computed 确认实际生效值是否符合预期，再回 Styles 追溯来源和冲突，效率最高。

Computed Styles 的作用确实很关键，要不要继续看看如何快速定位样式冲突的来源?或者盒模型图怎么帮助排查溢出问题?

## 自己样式优先级最高

控制台临时调试

- **直接改内联样式**‌：在 Elements 面板选中元素，右侧 Styles 里找到 `element.style`，直接写 `color: red  !important;`
- **用 `@layer` 级联层**‌，把自定义样式放在更高优先级的层里
