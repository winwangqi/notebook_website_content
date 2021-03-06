# 移动端开发总结

## 移动端开发实现自适应适配

### 解决方案1：rem

#### 版本1：meta scale 缩放 [ant-design-mobile:HD](https://github.com/ant-design/ant-design-mobile/wiki/HD)

##### 设置 viewport 和计算 root font size

*mete scale 会导致引用外部库缩放展示*

**压缩版**

```js:title=antm-viewport.min.js file=./scripts/antm-viewport.min.js
```

**未压缩版**

```js:title=antm-viewport.js file=./scripts/antm-viewport.js
```

##### px to rem

```js:title=webpack.config.js
// npm install postcss-pxtorem --save-dev
const pxtorem = require('postcss-pxtorem');
webpackConfig.postcss.push(pxtorem({
  rootValue: 100,
  propWhiteList: [],
}));
```

#### 版本2：flexible [lib-flexible](https://github.com/amfe/lib-flexible)

##### 设置 viewport 和计算 root font size

**压缩版**

```js:title=flexible.min.js file=./scripts/flexible.min.js
```

**未压缩版**

```js:title=flexible.js file=./scripts/flexible.js
```

##### px to rem

```js:title=webpack.config.js
// npm install postcss-pxtorem --save-dev
const pxtorem = require('postcss-pxtorem');
webpackConfig.postcss.push(pxtorem({
  rootValue: 75,
  propWhiteList: [],
}));
```

*postcss-pxtorem-exclude 包可以排除特定路径*

### 解决方案2：viewport

- [如何在Vue项目中使用vw实现移动端适配](https://juejin.im/entry/6844903571096338439)
- [evrone/postcss-px-to-viewport](https://github.com/evrone/postcss-px-to-viewport)

## 取消点击高亮

```css
* {
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
```


## 背景虚化

```css
selector {
  filter: blur(10px);
}

/* IOS 背景虚化 */
selector {
  -webkit-backdrop-filter: blur(10px);
}
```


## 1px 边框的实现
   
```less
.border-1px {
  position: relative;
}

.border-1px::after {
  display: block;
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  border-top: 1px solid @color;
  content: '';
}

@media (-webkit-min-device-pixel-ratio: 1.5), (min-device-pixel-ratio: 1.5) {
  .border-1px {
    &::after {
      -webkit-transform: scaleY(.7);
      transform: scaleY(.7);
    }
  }
}

@media (-webkit-min-device-pixel-ratio: 2), (min-device-pixel-ratio: 2) {
  .border-1px {
    &::after {
      -webkit-transform: scaleY(.5);
      transform: scaleY(.5);
    }
  }
}
```


## 消除 ios 输入框内阴影
   
```css
input, textarea {
  -webkit-appearance: none;
}
```


## ios 时间显示 NaN
   
### 问题描述

在 ios 系统下，实例化日期对象时，2017-08-14 10:30 时间格式会导致计算错误，出现 NaN 问题。

### 解决方法

在实例化时间对象之前，需要将时间连字符的 - 转换为 /。

```javascript
const originalTimeStr = '2017-08-14 10:30';
const uniTimeStr = originalTimeStr.replace(/\-/g, '/');
```


## iOS safari 开启物理惯性滚动支持

移动终端的开发中，在需要滚动的元素容器上，增加如下的css ，即可使滚动更平滑，并支持物理惯性的回弹。

```css
.scrolllist {
    -webkit-overflow-scrolling : touch;
}
```

Safari 会创建带有硬件加速的原生控件 UIScrollView 来实现此效果，使滚动更流畅。

注意：

移动终端的web开发适用，目前只有 IOS 的 Safari支持。

`-webkit-overflow-scrolling: touch;` 需要加到设置了 `overflow:scroll;` 的外层容器上。

Android 不支持，也不会支持，因为“已经滚动的足够快了”，相对来说缺少一个惯性回弹的效果。

[参考：网页在Safari快速滚动和回弹的原理： -webkit-overflow-scrolling : touch;的实现](http://blog.csdn.net/hursing/article/details/9186199)



## iPhoneX 屏幕适配

```css
@media only screen and (min-device-width : 360px) and (min-device-height : 740px) and (-webkit-min-device-pixel-ratio : 2.6) {
    /* ... */
}
```


## iPhoneX input placeholder 布局中

设置 line-height


## iPhoneX 全屏适配
   
### 问题描述

默认情况下，网页在 iPhoneX 的展示不会占满全屏

### 解决方法

针对 iPhoneX 特殊的屏幕，使用特有的属性来进行修复

在 HTML 的 meta:viewport 标签设置 viewport-fix 为 cover

```html
<meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
```

css 对应修改为

```css
body {
    padding-top: constant(safe-area-inset-top);
    padding-left: constant(safe-area-inset-left);
    padding-right: constant(safe-area-inset-right);
    padding-bottom: constant(safe-area-inset-bottom);
}
```

[参考：网页适配 iPhoneX，就是这么简单](https://aotu.io/notes/2017/11/27/iphonex/index.html)
