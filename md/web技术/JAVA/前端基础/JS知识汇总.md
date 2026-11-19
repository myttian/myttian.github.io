# JavaScript

## EventListener

[DOM EventListener ](https://www.runoob.com/js/js-htmldom-eventlistener.html)  

`addEventListener()` 是 JavaScript 里==为 DOM 元素绑定事件监听器==的标准方法，核心作用就是==让元素在触发特定事件（点击、输入、滚动等）时执行指定函数==。

### 基本用法

```javascript
element.addEventListener(event, function, useCapture);
//第一个参数是事件的类型 (如 "click" 或 "mousedown")
//第二个参数是事件触发后调用的函数
//第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的
```

- event：事件类型字符串，如 `"click"`、`"input"`、`"keydown"`，不带 `on` 前缀。
- function：事件触发时执行的回调函数。
- useCapture：可选布尔值，默认 `false`（冒泡阶段触发），设为 `true` 则在捕获阶段触发。

```javascript
const btn = document.getElementById('myBtn');
btn.addEventListener('click', function() {
  alert('按钮被点击了！');
});
```

### 核心特点

1. 可绑定多个监听器：同一元素可添加多个相同或不同类型的事件，不会互相覆盖。
2. 适用范围广：不限于 HTML 元素，也可用于 `window`、`document`、`XMLHttpRequest` 等对象。
3. 代码分离：将 JS 逻辑从 HTML 标记中分离，可读性和可维护性更好。

### 高级选项

第三个参数也可传对象，支持更多配置：

- `once: true`：监听器只执行一次后自动移除。
- `capture: true`：在捕获阶段触发。
- `passive: true`：提升滚动性能，告诉浏览器监听器不会调用 `preventDefault()`。

### 移除监听器

用 `removeEventListener()` 移除，必须传入与添加时完全相同的函数引用，匿名函数和箭头函数无法移除。

```javascript
function handleClick() {
  console.log('点了一次');
}
btn.addEventListener('click', handleClick);
btn.removeEventListener('click', handleClick); // ✅ 成功移除
```

### 注意事项

- `this` 指向：普通函数中 `this` 指向绑定事件的元素；箭头函数中继承外层作用域，不指向元素本身。
- 事件对象：回调函数自动接收 `event` 对象，可用 `event.target` 获取实际触发元素，`event.currentTarget` 获取绑定元素。
- 异步监听器：`async` 函数直接作为监听器时，内部错误不会冒泡到 `window.onerror` 或 `unhandledrejection`，需用 `try/catch` 或包装函数显式捕获。
- 内存管理：不再需要监听器时及时移除，避免内存泄漏。

addEventListener的高级用法挺有意思，要不要看看`once: true的作用`或者`passive: true`的适用场景

# JQuery

[韩顺平-javaWeb2022(JQuery笔记简)](https://blog.csdn.net/2301_76270413/article/details/133199319)   [jQuery ](https://www.cnblogs.com/lei0213/p/6114096.html)  

## 选择器相当于jquery函数参数吗?

不完全等同，但可以理解为“选择器是 jQuery 函数最常用的参数形式”。选择器本身只是字符串，只有作为参数传给 `$()` 或 `jQuery()` 时，才真正发挥作用。

### 两者的关系

1. 选择器是参数的一种：`$('#id')`、`$('.class')`、`$('div')` 这些写法，都是把 CSS 选择器字符串作为参数传入 `$` 函数，函数内部解析后返回匹配的 jQuery 对象。

2. `$` 函数接受多种参数：除了选择器字符串，还可以传 DOM 对象、HTML 字符串、函数等。
   - `$(function(){})` — 传函数，相当于 `$(document).ready()`
   - `$(domElement)` — 传原生 DOM 对象，包装成 jQuery 对象
   - `$('<div>html</div>')` — 传 HTML 字符串，创建新元素
   - `$('#id')` — 传选择器字符串，查找元素

3. 本质区别：选择器是数据（字符串），函数参数是接收数据的入口。选择器字符串本身没有行为，只有传入 `$()` 后，jQuery 内部通过 `jQuery.fn.init()` 解析并执行查找，才产生实际效果。

### 一句话理解

选择器是“你要找什么”的描述，函数参数是“怎么把描述交给 jQuery”的通道。日常写代码时，`$('div')` 就是把选择器作为参数传给 jQuery 核心函数，两者配合完成元素查找。

jQuery函数参数多样，可以看看除了选择器，还有哪些常见参数类型?或者函数参数和选择器的执行顺序是什么?

## 接受多种参数

除了选择器字符串，jQuery 的核心函数 `$()` 以及其各类方法还可以接受以下几种常见的参数类型。理解这些类型有助于更灵活地操作 DOM、处理事件和进行异步请求。

### DOM 元素或 DOM 元素数组

你可以直接将原生的 JavaScript DOM 对象或节点列表传递给 jQuery，将其包装成 jQuery 对象从而使用 jQuery 的方法。

* 单个 DOM 元素：

  ```javascript
  var nativeDiv = document.getElementById('myDiv');
  var $div = $(nativeDiv); // 将原生 DOM 转换为 jQuery 对象
  ```

* DOM 元素数组/集合：

  ```javascript
  var elements = document.querySelectorAll('p');
  var $paragraphs = $(elements); // 包装 NodeList 为 jQuery 对象
  ```

### HTML 字符串

传入包含 HTML 标签的字符串时，jQuery 会动态创建相应的 DOM 元素，并返回包含这些新元素的 jQuery 对象。这常用于动态添加内容。

* 创建新元素：

  ```javascript
  var $newDiv = $('<div class="box">Hello</div>');
  $('body').append($newDiv);
  ```

* 注意：如果字符串以 `<` 开头，jQuery 会尝试解析为 HTML；否则通常被视为选择器。

### 回调函数 (Function)

许多 jQuery 方法接受函数作为参数，用于在特定时刻执行逻辑，如文档加载完成、遍历元素或处理事件。

* 文档就绪函数：

  ```javascript
  $(function() {
      // 相当于 $(document).ready()，DOM 加载完成后执行
      console.log('DOM is ready');
  });
  ```

* 遍历与事件回调：

  ```javascript
  // .each() 遍历回调
  $('li').each(function(index, element) {
      console.log(index + ': ' + $(this).text());
  });
  
  // .on() 事件处理回调
  $('#btn').on('click', function() {
      alert('Clicked!');
  });
  ```

### 配置对象 (Object)

在涉及复杂操作（如 AJAX 请求、动画效果、批量设置样式/属性）时，通常传入一个键值对对象来配置行为。

* AJAX 请求配置：

  ```javascript
  $.ajax({
      url: '/api/data',
      type: 'GET',
      dataType: 'json',
      success: function(data) {
          console.log(data);
      },
      error: function(xhr, status, error) {
          console.error(error);
      }
  });
  ```

* 批量设置 CSS 或属性：

  ```javascript
  // 同时设置多个 CSS 属性
  $('.box').css({
      'color': 'red',
      'background-color': '#f0f0f0',
      'font-size': '16px'
  });
  
  // 同时设置多个 HTML 属性
  $('input').attr({
      'type': 'text',
      'placeholder': 'Enter name',
      'disabled': true
  });
  ```

### 总结

jQuery 的参数设计非常灵活，核心函数 `$()` 主要接收：

1.  选择器字符串（查找现有元素）
2.  HTML 字符串（创建新元素）
3.  DOM 元素/数组（包装原生对象）
4.  函数（文档就绪或逻辑回调）

而在具体的 jQuery 方法（如 `.css()`, `.ajax()`, `.on()`）中，对象和回调函数是最常见的参数形式，用于配置行为和定义后续操作。

FAQ

jQuery中还有哪些其他类型的参数
如何在jQuery中使用这些参数类型
jQuery中对象参数的常见用法有哪些
能否再列举一些常见的jQuery参数类型

<br>参考资料<br>[1] [jQuery参数列表集合_jquery-js教程-PHP中文网  - php中文网](https://www.php.cn/js-tutorial-20266.html)<br>[2] [请说出你可以传递给jQuery方法的四种不同值？-帅地玩编程 - www.iamshuaidi.com](https://www.iamshuaidi.com/44378.html)<br>[3] [jQuery.ajax() 方法核心参数详解-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/2531532)<br>[4] [jQuery参数列表集合_代码驿站 - www.codeinn.net](https://www.codeinn.net/misctech/23806.html)<br>[5] [深入解析：jQuery API文档全指南 - 百度智能云](https://cloud.baidu.com/article/3560250)<br>[6] [JQuery核心函数_百度百科 - 百度百科](https://baike.baidu.com/item/JQuery核心函数/10203879)<br>[7] [jQuery工具函数实战指南：类型判断、数据处理与老项目提效-CSDN博客 - CSDN博客](https://blog.csdn.net/rongdmmap/article/details/84171332)<br>[8] [深入理解JQuery Ajax：参数与回调详解 - 百家号](https://baijiahao.baidu.com/s?id=1847279172850247613&wfr=spider&for=pc)<br>[9] [超详细的jQuery的 DOM操作，一篇就足够！ - 知乎 - 知乎](https://zhuanlan.zhihu.com/p/375103214)<br>[10] [jQuery Ajax 全解析-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/1999662)<br>[11] [jQuery 选择器 | 菜鸟教程 - m.runoob.com](https://m.runoob.com/jquery/jquery-selectors.html)<br>[12] [jQuery 选择器：9 类核心选择器-CSDN博客 - CSDN博客](https://blog.csdn.net/2503_92319969/article/details/157360889)<br>[13] [jquery 常用方法总结-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/1881427)<br>[14] [JavaScript入门学习笔记（六）jQuery - 知乎 - 知乎](https://zhuanlan.zhihu.com/p/8621930149)<br>[15] [JavaScript与jQuery网页前端开发与设计_百度百科 - 百度百科](https://baike.baidu.com/item/JavaScript与jQuery网页前端开发与设计/22774832)<br>[16] [jquery中常用的函数和属性详细解析_jquery_脚本之家 - 脚本之家](https://www.jb51.net/article/47800.htm)<br>[17] [全网最新、最全的jQuery核心知识，你真的不想点开看看嘛？-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/1855419)<br>[18] [【JQuery】基础从零入门操作，简单详细-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/2482661)<br>[19] [【前端Vue3】——JQuery知识点总结（超详细）_vue3 jquery-CSDN博客 - CSDN博客](https://blog.csdn.net/shsjssnn/article/details/139307372)<br>[20] [蓝桥杯Web组知识点——jQuery篇_蓝桥杯考不考jquery-CSDN博客 - CSDN博客](https://blog.csdn.net/Lyy_ID/article/details/133901474)<br>[21] [jQuery多参数 jquery传递参数_mob6454cc6c6291的技术博客_51CTO博客 - 51CTO博客](https://blog.51cto.com/u_16099242/11556498)<br>[22] [jQuery 基本语法 day1 - 知乎 - 知乎](https://zhuanlan.zhihu.com/p/605971518)<br>[23] [jquery 数据类型 jquery参数_mob64ca13f34c58的技术博客_51CTO博客 - 51CTO博客](https://blog.51cto.com/u_16213563/9270639)<br>[24] [jQuery选择器和选取方法-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/2193084)<br>[25] [jQuery权威指南：实例全解析与源代码-CSDN博客 - CSDN博客](https://blog.csdn.net/weixin_42497762/article/details/142994351)<br>[26] [jQuery中文API速查表：开发者实用工具详解-CSDN博客 - CSDN博客](https://blog.csdn.net/weixin_28746457/article/details/149007971)<br>[27] [jquery some函数 jquery常用函数_mob6454cc7901c3的技术博客_51CTO博客 - 51CTO博客](https://blog.51cto.com/u_16099331/11767322)<br>[28] [jQuery_百度百科 - 百度百科](https://baike.baidu.com/item/jQuery/5385065)<br>[29] [【JQuery框架】五大选择器“全家桶”详解！！！-腾讯云开发者社区-腾讯云 - 腾讯云](https://cloud.tencent.com/developer/article/1992132)<br><br>百度AI生成，内容仅供参考

## jquery捕获动态元素

用 `on()` 方法的事件委托机制是 jQuery 捕获动态元素的标准做法。核心思路：将事件绑定到页面加载时已存在的静态父元素上，通过事件冒泡捕获动态子元素触发的事件，而非直接绑定到动态元素本身。

### 核心用法

基本语法：`$(静态父元素).on(事件类型, 动态子元素选择器, 处理函数)`

```javascript
// 绑定到离动态元素最近的静态父元素（推荐）
$('#list').on('click', 'li', function() {
    console.log($(this).text()); // this 指向被点击的 li
});

// 或者绑定到 document（最通用，但性能略差）
$(document).on('click', '.btn-del', function() {
    // 处理删除逻辑
});
```

### 关键要点

1. 绑定时机：事件绑定代码在页面加载时执行，此时动态元素尚未存在，直接绑定会失效。
2. 选择器精度：子元素选择器尽量用 class 而非标签名，避免误伤其他元素。
3. this 指向：处理函数内 `this` 指向触发事件的动态元素本身，可直接用 `$(this)` 操作。
4. 不冒泡事件：`focus`、`blur` 不冒泡，需用 `focusin`、`focusout` 替代。

### 完整示例

```javascript
// 动态添加元素
$('#addBtn').on('click', function() {
    $('#list').append('<li class="item">动态项</li>');
});

// 事件委托：捕获动态 li 的点击
$('#list').on('click', '.item', function() {
    alert($(this).text());
    $(this).remove();
});
```

### 方法对比

| 方法         | 支持动态元素 | 说明                         |
| ------------ | ------------ | ---------------------------- |
| `bind()`     | ❌            | 仅绑定页面加载时已存在的元素 |
| `live()`     | ✅            | jQuery 1.9 已废弃，勿用      |
| `delegate()` | ✅            | 可无事件，但已被 `on()` 替代 |
| `on()`       | ✅            | 1.7+ 推荐方式，整合以上所有  |

> `on()` 方法本质上是将监听器挂到父元素，事件冒泡到父元素时检查事件源是否匹配选择器，因此无论动态添加多少元素都能被捕获。

事件委托是 jQuery 的核心技巧，想深入了解的话，可以看看事件冒泡机制如何实现委托捕获?或者为什么 bind 和 live 方法不支持动态元素?

# ECMA

[es10,es11,es12特性介绍](https://cloud.tencent.com/developer/article/2646174)  [ES12语法](https://cloud.tencent.com/developer/article/2168602)   

[js版本ES6、ES7、ES8、ES9、ES10、ES11、ES12、ES13、ES14[2023]新特性](https://www.jb51.net/javascript/329890ltu.htm)  