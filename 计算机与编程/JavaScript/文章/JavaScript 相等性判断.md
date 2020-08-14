# JavaScript 相等性判断

## 1. 全等（===）比较规则

- 如果两个值类型不相等，则它们不相等。
- 值类型相等时才去判断它们的值是否相等。
- NaN 与任何值都不相等，包括它本身。
    ```js
    NaN === NaN     // false
    ```
- 0、+0、-0 三者互相全等
    ```js
     0 === -0       // true
     0 === +0       // true
    -0 === +0       // true
    ```
- 两个引用值指向同一个对象时才相等。
    ```
    即使两个对象具有一样的属性也不相等。
    ```

## 2. 非严格相等（==）比较规则

**"==" 运算符从不试图将其操作数转换为布尔值**

- 【null】与【undefined】

    ```
    null == undefined   // true

    在比较相等性之前，不能将 null 和 undefined 转换为其它任何值。
    
    null == true        // false
    null == false       // false
    undefined == true   // false
    undefined == false  // false

    null, undefined 在比较运算中，并不将其转换为数字再比较，而就是拿其本身来比较！
    Number(null)        // => 0
    Number(undefined)   // => NaN
    
    在 javascript 中，undefined 衍生自 null，所以null 与 undefined 天生相等。
    当然，null !== undefined
    ```

- 【数字】与【字符串】

    ```
    1. 将字符串转换为数字
    2. 使用转换后的值进行比较
    ```

- 【true】与【false】

    ```
    1. 将 true  转换为 1 后进行比较
    2. 将 false 转换为 0 后进行比较
    ```

- 【对象】与【数字或字符串】

    ```
    将对象转换为原始值，然后再进行比较。
    ```

    **请注意！**

    ```js
    Boolean([])     // true，别以为 [] 转为换为布尔值的结果是 true 就与布尔值 true 就相等，并没有卵的关系！！！
    [] == true      // false，要比较，一切化归为数字说话！
    Number([])      // 0
    [] == false     // true

    true  == {}     // false
    false == {}     // false
    Number({})      // NaN，过程为：{}.toSting() => "[object Object]" => NaN
    ```

**最后请记住三句话：**

1. 相等性判断与类型转换并**没有什么关系**，只能依据以上的规则来判断！
2. "==" 运算符**从不试图**将其操作数转换为布尔值
3. 一个值与 true 不相等，则它必然与 false 相等。（这句话，**错的，错的！！**）

---
参考资料：

    《JavaScript 权威指南》 （第6版） [美].David Flanagan著 淘宝前端团队译
    《JavaScript 高级程序设计》 （第3版） [美].Nicholas C.Zakas著 李松峰 曹力译
