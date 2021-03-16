# Web 基础

## URI 与 URL

### URI 与 URL 的关系

URI是一类更通用的资源标识符，URL实际上是它的一个子集。URI是一个通用的概念，由两个主要的子集URL和URN构成，URL是通过描述资源的位置来标识资源的，而URN（本章稍后会介绍）则是通过名字来识别资源的，与它们当前所处位置无关。

### URL 的语法

```
<schema>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>

http://user:password@example.com:80/index;type=d?foo=bar#baz
```