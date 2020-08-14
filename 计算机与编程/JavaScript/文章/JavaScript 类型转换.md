# JavaScript 类型转换

## 1. to Number

### 1.1 parseInt()

- 仅针对字符串

    ```
    1. 忽略字符串前面的空格，直到找到第一个非空格符

    2. 如果第一个字符不是数字或负号，返回 NaN

        parseInt("") => NaN

    3. 如果第一个字符是数字字符，继续解析第二个字符，直到解析完所有后续字符或遇到一个非数字字符

        parseInt("9527great") => 9527
        parseInt("11.4") => 11

    4. 可以识别出各种整数字符（十进制、八进制、十六进制）

        parseInt("0xA") => 10
        parseInt("070") => 56
        
        在解析八进制时，ES3 和 ES5 存在分歧，为消除不必要的麻烦，建议传入第二个参数以表示转换时使用的基数（即进制数）

        parseInt("070",  8) => 56   // 当作八进制数来解析
        parseInt("070", 10) => 70   // 当作十进制数来解析
    ```

### 1.2 parseFloat()

- 仅针对字符串

    ```
    1. 忽略字符串前面的空格，直到找到第一个非空格符

    2. 如果第一个字符不是数字或负号，返回 NaN

        parseFloat("") => NaN

    3. 从位置 0 开始解析每个字符，一直解析到字符串末尾，或解析遇到一个无效的浮点数字符为止

        parseFloat("9527.23great") => 9527.23

    4. 第一个小数点有效，第二个小数点无效

        parseFloat("22.34.56") => 22.34

    5. 始终会忽略前导的 0

        parseFloat("0729.4") => 729.4

    6. 只解析十进制整数格式

        无第二个参数指定基数的用法
        十六进制格式的字符串始终会被解析成 0

        parseFloat("0xF") => 0
        parseFloat("3.12e7") => 31200000
    ```

### 1.3 Number()

- boolean

    ```
    Number(true)  => 1
    Number(false) => 0
    ```

- number

    ```
    只是简单的传入与传出

    Number(2) => 2
    ```

- null

    ```
    Number(null) => 0
    ```

- undefined

    ```
    Number(undefined) => NaN
    ```

- string

    ```
    1. 只包含数字，将其转换为十进制

        Number("1") => 1
        Number("011") => 11

    2. 包含有效的浮点格式，将其转换为对应的浮点数值

        Number("1.1") => 1.1
        Number("02.3") => 2.3

    3. 包含有效的十六进制格式，将其转换为相同大小的十进制数

        Number("0xf") => 15

    4. 空字符串，将其转换为 0

        Number("") => 0

    5. 其它格式字符串，将其转换为 NaN

        Number("2.2a") => NaN
    ```

- 对象

    ```
    如果是对象，则调用对象的 valueOf() 方法，然后依照前面的规则转换返回的值。
    如果转换的结果是 NaN，则调用对象的 toString() 方法，然后再次依照前面的规则转换返回的字符串值。

    Number({}) => NaN    过程：{}.toString() => "[object Object]" => NaN
    ```

### 1.4 隐式转换

> 等价于 Number(x)

- +x

- x - 0

---

## 2. to String

### 2.1 toString()

- number、boolean、object、string 都有 toString() 方法

- 数值的 toString() 方法可以传递一个参数指定输出数值的基数

- null 和 undefined 没有 toString() 方法


### 2.2 String()

- String() 转型函数能够将任何类型的值转换为字符串

- 转换规则

    ```
    1. 如果值有 toString() 方法，则调用该方法并返回相应的结果
    
    2. 如果值是 null，则返回 "null"
    
    3. 如果值是 undefined，则返回 "undefined"
    ```
    
### 2.3 隐式转换

> 等价于 String(x)

- x + ""

### 2.4 number-to-string

- toFixed()
> 根据小数点后的指定位数将数字转换为字符串，它从不使用指数记数法。

- toExponential()

- toPrecision()




---

## 3. to Boolean

### 3.1 Boolean()

- boolean

    ```
    Boolean(true)  => true
    Booelan(false) => false
    ```

- string

    ```
    Boolean("") => false
    Boolean("非空字符") => true
    ```

- number

    ```
    Boolean(0)   => false
    Boolean(NaN) => false
    Boolean(非零数字值) => true
    ```

- object

    ```
    Boolean(null) => false
    Boolean(任何对象) => true
    ```

- undefined

    ```
    Boolean(undefined) => false
    ```

### 3.2 隐式转换

> 等价于 Boolean(x)

- !!x


|值|转换为字符串|数字|布尔值|对象|
|---|---|---|---|---|
|undefined|"undefined"|NaN|false|throws TypeError|
|null|"null"|0|false|throws TypeError|
|---------------------------|-------------------|-------|--------|---------------------------|
|true|"true"|1||new Boolean(true)|
|false|"false"|0||new Boolean(false)|
|---------------------------|-------------------|-------|--------|---------------------------|
|""||0|false|new String("")|
|"1.2"||1.2|true|new String("1.2")|
|"one"||NaN|true|new String("one")|
|---------------------------|-------------------|-------|--------|---------------------------|
|0|"0"||false|new Number(0)|
|-0|"0"||false|new Number(-0)|
|NaN|"NaN"||false|Number(NaN)|
|Infinity|"Infinity"||true|new Number(Infinity)|
|-Infinity|"-Infinity"||true|new Number(-Infinity)|
|1|"1"||true|new Number(1)|
|---------------------------|-------------------|-------|--------|---------------------------|
|{}(任意对象)|||true||
|\[](任意数组)|""|0|true||
|\[9](1个数字元素)|"9"|9|true||
|\["a"](其他数组)|使用 join() 方法|NaN|true||
|function(){}(任意函数)||NaN|true||
