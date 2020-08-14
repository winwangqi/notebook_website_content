# JavaScript 中的数字 Number 易于忽略点

## 一、浮点数

### 1. 浮点数的存储

- 保存浮点数值需要的内存空间是保存整数值的两倍，因此 ECMAScript 会不失时机地将浮点数值转换为整数值。例如：
	
	```javascript
	var floatNum1 = 1.;	// 小数点后面没有数字——解析为 1
	var floatNum2 = 10.0;	// 整数——解析为 10
	```

- 可以使用指数记数法表示浮点型直接量，即在实数后跟字母 e 或 E，后面再跟正负号，其后再加一个整型的指数。语法表示为：

    `[digits][.digits][(E|e)[(+|-)]digits]`

    例如：

	```javascript
	6.02e23 	// 6.02 * 10^23
	```


### 2. 浮点数的运算

- **0.1 + 0.2 != 0.3**

	这是使用基于 IEEE754 数值的浮点计算的通病！

	> 解决方案：先将浮点数转换为整数后进行运算，然后再转换为小数  
	> 例如：(0.1 \* 10 + 0.2 \* 10) / 10 === 0.3


## 二、数值范围

### 1. 最大值 & 最小值

- 最大值  

	保存在 `Number_MAX_VALUE` 中，值为：1.7976931348623157e+308

- 最小值  

	保存在 `Number_MIN_VALUE` 中，值为：5e-324

	> 注意：此处的最小值并不是我们通常理解的值很小的负数，而是无限接近于 0 的正数。

### 2. 正无穷 & 负无穷

- 正无穷：`Number_POSITIVE_INFINITY  `

- 负无穷：`Number_NEGATIVE_INFINITY`

### 3. 溢出 & 下溢

- 溢出（overflow）

	> 大于 Number_MAX_VALUE，为 `Infinity`

	> 小于 -Number_MAX_VALUE，为 `-Infinity`  

- 下溢（underflow）

	> 无限接近于 0，并比 Number_MIN_VALUE 还小的值，返回 0。 

	> 即：`[ -Number_MIN_VALUE, Number_MIN_VALUE ]`

---

## 三、NaN

NaN，即非数值（Not a Number）是一个特殊的数值，这个数值用于表示一个本来要返回数值的操作数未返回数值的情况。

**NaN 与任何值都不相等，包括 NaN 本身！！！**


## 四、 特殊计算

1. +num / 0 = Infinity

2. -num / 0 = -Infinity

3. 1 / Infinity = 0

4. 0 / 0 = NaN

## 五、Math 对象的属性

| 属性&方法 | 说明 |
|----------|----------|
| Math.E | e：自然对数的底数 |
| Math.sqrt(3) | 3 的平方根 |
| Math.log(3) | 3 的自然对数 |
| Math.exp(3) | e 的三次幂 |
|  Math.pow(2, 13)  |  2 的 13 次幂  |
| Math.pow(3, 1/3) | 3 的立方根 |
其中只列出了不熟悉的属性和方法。
