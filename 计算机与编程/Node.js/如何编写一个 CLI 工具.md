# 如何编写一个 CLI 工具

## 背景知识

### [Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))

在计算领域中，**Shebang**（也称为Hashbang）是一个由井号和叹号构成的字符序列 `#!`，其出现在文本文件的第一行的前两个字符。 在文件中存在 Shebang 的情况下，类 Unix 操作系统的程序加载器会分析 Shebang 后的内容，将这些内容作为解释器指令，并调用该指令，并将载有 Shebang 的文件路径作为该解释器的参数。


## 工具包

- [Commander.js]: node.js command-line interfaces made easy.
- [yargs]: Yargs helps you build interactive command line tools, by parsing arguments and generating an elegant user interface.
- [Inquirer.js]: A collection of common interactive command line user interfaces.
- [chalk]: 🖍 Terminal string styling done right.

[Commander.js]: https://github.com/tj/commander.js
[yargs]: https://github.com/yargs/yargs
[Inquirer.js]: https://github.com/SBoudrias/Inquirer.js
[chalk]: https://github.com/chalk/chalk


## 参考

- [从0到1开发一个小程序cli脚手架（一）--创建页面/组件模版篇](https://juejin.cn/post/6844903892170309646) 
- [从0到1开发一个小程序cli脚手架（二）--版本发布/管理篇](https://juejin.cn/post/6844903906363834375) 

