# 前端开发面试 - JavaScript

## `<script>` 标签 `async` 和 `defer` 的却别

`async`

该布尔属性指示浏览器是否在允许的情况下异步执行该脚本。该属性对于内联脚本无作用 (即没有src属性的脚本）。也就是说，async属性告诉浏览器先把文件下载下来，在“时机成熟”的时候再执行。异步脚本一定会在页面的load事件前执行，但可能会在DOMContentLoaded事件触发之前或之后执行。而且更加需要注意的是，标记为async的脚本并不保证按照指定他们的先后顺序执行。所以，确保各个异步脚本互不依赖非常重要。

`defer`

这个布尔属性被设定用来通知浏览器该脚本将在文档完成解析后，触发 `DOMContentLoaded` 事件前执行。如果缺少 `src` 属性（即内嵌脚本），该属性不应被使用，因为这种情况下它不起作用。对动态嵌入的脚本使用 `async=false` 来达到类似的效果。

HTML5 规范要求脚本按照它们出现的先后顺序执行，因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于 `DOMContentLoaded` 事件执行。在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 `DOMContentLoaded` 事件触发前执行，因此最好只包含一个延迟脚本。

[参考](https://zhuanlan.zhihu.com/p/30898865#:~:text=Async%E6%98%AF%E5%9C%A8%E5%A4%96%E9%83%A8JS,%E6%96%87%E4%BB%B6%EF%BC%8C%E6%89%80%E4%BB%A5%E5%8F%AF%E4%BB%A5%E8%8A%82%E7%9C%81%E6%97%B6%E9%97%B4%E3%80%82)

## 事件循环

- [浏览器与Node的事件循环(Event Loop)有何区别?](https://juejin.cn/post/6844903761949753352)
- [Node.js 事件循环，定时器和 `process.nextTick()`](https://nodejs.org/zh-cn/docs/guides/event-loop-timers-and-nexttick/)

## `new` 运算符

- [new 运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)

## 自定义事件

- [创建和触发 events](https://developer.mozilla.org/zh-CN/docs/Web/Guide/Events/Creating_and_triggering_events)

## [setTimeout、Promise、Async/Await 的区别](https://muyiy.cn/question/async/8.html)

## 模块化

- [模块化思维导图](https://www.processon.com/view/link/5c8409bbe4b02b2ce492286a#map)
