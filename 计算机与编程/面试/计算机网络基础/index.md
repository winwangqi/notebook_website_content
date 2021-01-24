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

## 缓存

- [强制缓存和协商缓存](https://juejin.cn/post/6844903838768431118)
- [缓存（二）——浏览器缓存机制：强缓存、协商缓存](https://github.com/amandakelake/blog/issues/41)

## HTTPS

- [你连 HTTPS 原理都不懂,还讲“中间人攻击”?](https://juejin.cn/post/6844904065227292685)