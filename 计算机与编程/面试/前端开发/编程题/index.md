# 前端开发面试 - 编程题

## [Function.prototype.bind()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

```JavaScript
//  Yes, it does work with `new (funcA.bind(thisArg, args))`
if (!Function.prototype.bind) (function () {
  var ArrayPrototypeSlice = Array.prototype.slice;
  Function.prototype.bind = function (otherThis) {
    if (typeof this !== 'function') {
      // closest thing possible to the ECMAScript 5
      // internal IsCallable function
      throw new TypeError('Function.prototype.bind - what is trying to be bound is not callable');
    }

    var baseArgs = ArrayPrototypeSlice.call(arguments, 1),
      baseArgsLength = baseArgs.length,
      fToBind = this,
      fNOP = function () { },
      fBound = function () {
        baseArgs.length = baseArgsLength; // reset to default base arguments
        baseArgs.push.apply(baseArgs, arguments);
        return fToBind.apply(
          fNOP.prototype.isPrototypeOf(this) ? this : otherThis, baseArgs
        );
      };

    if (this.prototype) {
      // Function.prototype doesn't have a prototype property
      fNOP.prototype = this.prototype;
    }
    fBound.prototype = new fNOP();

    return fBound;
  };
})();
```

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

## `add(1)(2)(3)()`

### 描述

实现一个 `add` 函数，实现如下功能：

```JavaScript
add(1)() // 1
add(1)(2)() // 3
add(1)(2)(3)() // 6
add(1)(2, 3)() // 6
add(1, 2)(3)() // 6
add(1, 2, 3)() // 6
```

### 实现

```JavaScript
function add(...args) {
  return function (...subArgs) {
    if (subArgs.length === 0) {
      return args.reduce((acc, cur) => acc + cur)
    }

    return add.apply(null, args.concat(subArgs))
  }
}
```


## 实现 `Promise`

- [自己动手实现一个 Promise](https://xie.infoq.cn/article/c8a84e175fb14b8abbd68172f)


## 实现一个带并发限制的异步调度器 Scheduler

### 描述

```JavaScript
// 实现一个带并发限制的异步调度器 Scheduler
// 保证同时运行的任务最多有两个
// 完善代码中Scheduler类
// 使得以下程序能正确输出

class Scheduler {
	constructor() {
		
	}

	add(task) {

	}
}


const timeout = (time) => new Promise(resolve => {
	setTimeout(resolve, time)
})

const scheduler = new Scheduler()
const addTask = (time, order) => {
	scheduler.add(() => timeout(time)).then(() => console.log(order))
}

addTask(1000, '1')
addTask(500, '2')
addTask(300, '3')
addTask(400, '4')
// output: 2 3 1 4

// 一开始，1、2两个任务进入队列
// 500ms时，2完成，输出2，任务3进队
// 800ms时，3完成，输出3，任务4进队
// 1000ms时，1完成，输出1
// 1200ms时，4完成，输出4
```

### 实现

```JavaScript
class Scheduler {
  concurrency = 2
  taskQueue = []
  runningTasks = []

  add(task) {
    this.taskQueue.push(task)
    return this.next()
  }

  next() {
    if (this.taskQueue.length > 0 && this.runningTasks.length < this.concurrency) {
      const task = this.taskQueue.shift()

      const promise = task().then((value) => {
        this.runningTasks = this.runningTasks.filter(v => v !== promise)
        return value
      })
  
      this.runningTasks.push(promise)
  
      return promise
    } else {
      return Promise.race(this.runningTasks).then(() => this.next())
    }
  }
}
const timeout = (time) => new Promise(resolve => {
  setTimeout(resolve, time)
})
const scheduler = new Scheduler()

const addTask = (time, order) => {
  scheduler.add(() => timeout(time)).then(() => console.log(order))
}

addTask(1000, '1')
addTask(500, '2')
addTask(300, '3')
addTask(400, '4')
// output: 2 3 1 4 
// 一开始，1、2两个任务进入队列 
// 500ms时，2完成，输出2，任务3进队 
// 800ms时，3完成，输出3，任务4进队 
// 1000ms时，1完成，输出1 
// 1200ms时，4完成，输出4

// 最大核心数
// 当任务完成，已完成任务出队，新任务进队
// 当任务完成，通知调度器
```


## LazyMan

### 描述

设计 LazyMan 类，实现如下功能：

```JavaScript
LazyMan('Tony');
// Hi I am Tony

LazyMan('Tony').sleep(10).eat('lunch');
// Hi I am Tony
// 等待了10秒...
// I am eating lunch

LazyMan('Tony').eat('lunch').sleep(10).eat('dinner');
// Hi I am Tony
// I am eating lunch
// 等待了10秒...
// I am eating diner

LazyMan('Tony').eat('lunch').eat('dinner').sleepFirst(5).sleep(10).eat('junk food');
// Hi I am Tony
// 等待了5秒...
// I am eating lunch
// I am eating dinner
// 等待了10秒...
// I am eating junk food
```

### 实现

```JavaScript
class LazyManClass {
  constructor(name) {
    this.name = name
    this.queue = []
    console.log(`Hi I am ${name}`)
    setTimeout(() => {
      this.next()
    },0)
  }

  sleepFirst(time) {
    const fn = () => {
      setTimeout(() => {
        console.log(`等待了${time}秒...`)
        this.next()
      }, time)
    }
    this.queue.unshift(fn)
    return this
  }

  sleep(time) {
    const fn = () => {
      setTimeout(() => {
        console.log(`等待了${time}秒...`)
        this.next()
      },time)
    }
    this.queue.push(fn)
    return this
  }

  eat(food) {
    const fn = () => {
      console.log(`I am eating ${food}`)
      this.next()
    }
    this.queue.push(fn)
    return this
  }

  next() {
    const fn = this.queue.shift()
    fn && fn()
  }
}

function LazyMan(name) {
  return new LazyManClass(name)
}
```
