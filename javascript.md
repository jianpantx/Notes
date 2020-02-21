### undefined 和 null

```
null 表示控制
undefined 表示未定义
```



Javascript 没有整数 多有数字都是以64位浮点数形式存储 

```javascript
1 === 1.0 
```

```javascript
0.1 + 0.2 === 0.3 //false
0.3/0.1 //2.9999999999999996
(0.3 - 0.2) === (0.2 - 0.1)
// false
```



### 数值精度

JavaScript 提供的有效数字最长为53个二进制位

精度最多只能到53个二进制位，这意味着，绝对值小于2的53次方的整数，即-253到253，都可以精确表示

```javascript
Math.pow(2, 53)
// 9007199254740992

Math.pow(2, 53) + 1
// 9007199254740992

Math.pow(2, 53) + 2
// 9007199254740994

Math.pow(2, 53) + 3
// 9007199254740996

Math.pow(2, 53) + 4
// 9007199254740996
```

由于2的53次方是一个16位的十进制数值，所以简单的法则就是，JavaScript 对15位的十进制数都可以精确处理。 



### 数值范围

根据标准，64位浮点数的指数部分的长度是11个二进制位，意味着指数部分的最大值是2047（2的11次方减1）。也就是说，64位浮点数的指数部分的值最大为2047，分出一半表示负数，则 JavaScript 能够表示的数值范围为21024到2-1023（开区间），超出这个范围的数无法表示。

```javascript
Math.pow(2, 1024) // Infinity
```

```javascript
Math.pow(2, -1075) // 0
```

avaScript 提供`Number`对象的`MAX_VALUE`和`MIN_VALUE`属性，返回可以表示的具体的最大值和最小值。

```javascript
Number.MAX_VALUE // 1.7976931348623157e+308
Number.MIN_VALUE // 5e-324txzs
```



### 正零和负零

几乎所有场合，正零和负零都会被当作正常的`0`

```javascript
-0 === +0 // true
0 === -0 // true
0 === +0 // true
+0 // 0
-0 // 0
(-0).toString() // '0'
(+0).toString() // '0'
```

唯一区别场合是当分母的时候

```javascript
(1 / +0) === (1 / -0) // false
```

上面的代码之所以出现这样结果，是因为除以正零得到`+Infinity`，除以负零得到`-Infinity`，这两者是不相等的



 ### NaN

`NaN`是 JavaScript 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。

```javascript
5 - 'x' // NaN
```

上面代码运行时，会自动将字符串`x`转为数值，但是由于`x`不是数值，所以最后得到结果为`NaN`，表示它是“非数字”（`NaN`）。

数学函数运算

```javascript
Math.acos(2) // NaN
Math.log(-1) // NaN
Math.sqrt(-1) // NaN
```

`0`除以`0`也会得到`NaN`。

```javascript
0除以0也会得到NaN。
```



> 需要注意的是，`NaN`不是独立的数据类型，而是一个特殊数值，它的数据类型依然属于`Number`，使用`typeof`运算符可以看得很清楚。

```javascript
typeof NaN // 'number'
```



#####  `NaN`不等于任何值，包括它本身。

`NaN`与任何数（包括它自己）的运算，得到的都是`NaN`。

```javascript
NaN + 32 // NaN
NaN - 32 // NaN
NaN * 32 // NaN
NaN / 32 // NaN
```



### Infinity(无穷大)

表示两种场景。一种是一个正的数值太大，或一个负的数值太小，无法表示；另一种是非0数值除以0，得到`Infinity`。

```javascript
// 场景一
Math.pow(2, 1024)
// Infinity 超出表示范围

// 场景二
0 / 0 // NaN
1 / 0 // Infinity
```



`Infinity`有正负之分，`Infinity`表示正的无穷，`-Infinity`表示负的无穷。

非零正数除以`-0`，会得到`-Infinity`，负数除以`-0`，会得到`Infinity`。

```javascript
Infinity === -Infinity // false

1 / -0 // -Infinity
-1 / -0 // Infinity
```



`Infinity`大于一切数值（除了`NaN`），`-Infinity`小于一切数值（除了`NaN`）。

```javascript
Infinity > 1000 // true
-Infinity < -1000 // true
```



`Infinity`与`NaN`比较，总是返回`false`。

```javascript
Infinity > NaN // false
-Infinity > NaN // false

Infinity < NaN // false
-Infinity < NaN // false
```



>自己总结 除NaN、Infinity自身、undefined以外 Infinity为分子，结果都为Infinity；Infinity为分母, 结果都为0

```javascript
5 * Infinity // Infinity
5 - Infinity // -Infinity
Infinity / 5 // Infinity
5 / Infinity // 0

0 * Infinity // NaN
0 / Infinity // 0
Infinity / 0 // Infinity

null * Infinity // NaN
null / Infinity // 0
Infinity / null // Infinity

undefined + Infinity // NaN
undefined - Infinity // NaN
undefined * Infinity // NaN
undefined / Infinity // NaN
Infinity / undefined // NaN

Infinity - Infinity // NaN
Infinity / Infinity // NaN
```



### 与数值相关的全局方法

##### parseInt()

`parseInt`的返回值只有两种可能，要么是一个十进制整数，要么是`NaN`。

```javascript
parseInt(1000000000000000000000.5) // 1
// 等同于
parseInt('1e+21') // 1

parseInt(0.0000008) // 8
// 等同于
parseInt('8e-7') // 8

parseInt(0.000008) // 0
```

进制转换

`parseInt`方法还可以接受第二个参数（2到36之间），表示被解析的值的进制，返回该值对应的十进制数。默认情况下，`parseInt`的第二个参数为10，即默认是十进制转十进制。

```javascript
parseInt('1000') // 1000
// 等同于
parseInt('1000', 10) // 1000

parseInt('1000', 2) // 8
parseInt('1000', 6) // 216
parseInt('1000', 8) // 512

parseInt('10', 37) // NaN
parseInt('10', 1) // NaN
parseInt('10', 0) // 10
parseInt('10', null) // 10
parseInt('10', undefined) // 10
```



### Base64 转码

JavaScript 原生提供两个 Base64 相关的方法。

- `btoa()`：任意值转为 Base64 编码
- `atob()`：Base64 编码转为原来的值

> 注意，这两个方法不适合非 ASCII 码的字符，会报错。

```javascript
var string = 'Hello World!';
btoa(string) // "SGVsbG8gV29ybGQh"
atob('SGVsbG8gV29ybGQh') // "Hello World!"

btoa('你好') // 报错
```

要将非 ASCII 码字符转为 Base64 编码，必须中间插入一个转码环节，再使用这两个方法。

```javascript
function b64Encode(str) {
  return btoa(encodeURIComponent(str));
}

function b64Decode(str) {
  return decodeURIComponent(atob(str));
}

b64Encode('你好') // "JUU0JUJEJUEwJUU1JUE1JUJE"
b64Decode('JUU0JUJEJUEwJUU1JUE1JUJE') // "你好"
```



### 关于对象

如果不同的变量名指向同一个对象，那么它们都是这个对象的引用，也就是说指向同一个内存地址。修改其中一个变量，会影响到其他所有变量。

```javascript
var o1 = {};
var o2 = o1;

o1.a = 1;
o2.a // 1

o2.b = 2;
o1.b // 2

var o1 = {};
var o2 = o1;

o1 = 1;
o2 // {}
```

这种引用只局限于对象，如果两个变量指向同一个原始类型的值。那么，变量这时都是值的拷贝。

```javascript
var x = 1;
var y = x;

x = 2;
y // 1
```



### 函数

函数是一个可以执行的值