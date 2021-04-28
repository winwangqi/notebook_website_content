# 计算机网络基础

## TCP

什么是 TCP，三次握手，四次挥手

- [TCP 协议](https://hit-alibaba.github.io/interview/basic/network/TCP.html)
- [TCP 为什么三次握手而不是两次握手](https://blog.csdn.net/lengxiao1993/article/details/82771768)

### 三次握手

三次握手之所以是三次是保证client和server均让对方知道自己的接收和发送能力没问题而保证的最小次数。

第一次 client => server 只能server判断出client具备发送能力
第二次 server => client client就可以判断出server具备发送和接受能力。此时client还需让server知道自己接收能力没问题于是就有了第三次
第三次 client => server 双方均保证了自己的接收和发送能力没有问题

其中，为了保证后续的握手是为了应答上一个握手，每次握手都会带一个标识 seq，后续的ACK都会对这个seq进行加一来进行确认。

### 四次挥手


## 缓存

- [强制缓存和协商缓存](https://juejin.cn/post/6844903838768431118)
- [缓存（二）——浏览器缓存机制：强缓存、协商缓存](https://github.com/amandakelake/blog/issues/41)

## HTTPS

- [你连 HTTPS 原理都不懂,还讲“中间人攻击”?](https://juejin.cn/post/6844904065227292685)


## 网络安全

### [XSS 跨站脚本攻击](https://zh.wikipedia.org/wiki/%E8%B7%A8%E7%B6%B2%E7%AB%99%E6%8C%87%E4%BB%A4%E7%A2%BC)

跨站脚本是一种网站应用程序的安全漏洞攻击，是代码注入的一种。它允许恶意用户将代码注入到网页上，其他用户在观看网页时就会受到影响。这类攻击通常包含了HTML以及用户端脚本语言。

#### 防范

- 过滤特殊字符


### [CSRF 跨站请求伪造](https://zh.wikipedia.org/wiki/%E8%B7%A8%E7%AB%99%E8%AF%B7%E6%B1%82%E4%BC%AA%E9%80%A0)

跨站请求伪造是一种挟制用户在当前已登录的Web应用程序上执行非本意的操作的攻击方法。

#### 防范

- 令牌同步模式
- 检查 `Referer` 字段
- 添加校验 `token`


## HTTP2