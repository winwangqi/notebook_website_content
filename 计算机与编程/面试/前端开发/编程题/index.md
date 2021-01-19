# 前端开发面试 - 编程题

## `bind`

- [Function.prototype.bind()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

## `debounce` 和 `throttle`

- [函数防抖和函数节流（debounce and throttle）](https://juejin.cn/post/6844904129215610888)
- [JavaScript 专题之跟着 underscore 学防抖](https://github.com/mqyqingfeng/Blog/issues/22)
- [JavaScript 专题之跟着 underscore 学节流](https://github.com/mqyqingfeng/Blog/issues/26)

### `debounce`

```javascript
function debounce(fn,delay,immediate) {
  let timer;
  return function () {
    let that = this;
    let args = arguments;
    if (timer) clearTimeout(timer);
    if (immediate) { // 这里设置是否启用立即执行
      let able = !timer;
      timer = setTimeout(() => {
        timer = null;
      }, delay)
      if (able) fn.apply(that, args)
    } else {
      timer = setTimeout(()=>{
        fn.apply(that, args)
      }, delay);
    }
  }
}
```

### `throttle`

```javascript
function throttle(fn, delay, immediate) {
  let timer;
  return function() {
    let that = this;
    let args = arguments;
    if (!timer) {
      if(immediate){
        fn.apply(that, args)
        timer = setTimeout(() => {
          timer = null;
        }, delay)
      }else {
        timer = setTimeout(() => {
          timer = null;
          fn.apply(that, args)
        }, delay)
      }
    }
  }
}
```

## [模拟实现一个 `Promise.finally`](https://muyiy.cn/question/async/64.html)

## [实现 (5).add(3).minus(2)](https://muyiy.cn/question/program/50.html)

## [请实现一个 add 函数，add(1)(2)(3)](https://muyiy.cn/question/program/84.html)

## 实现 `Promise`

- [自己动手实现一个 Promise](https://xie.infoq.cn/article/c8a84e175fb14b8abbd68172f)
