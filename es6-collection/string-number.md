# ES6笔记(String/Number)


## String

### at()
ES5: chartAt(),   
ES6: at()

````
'abc'.charAt(0) // "a"
'𠮷'.charAt(0) // "\uD842"


'abc'.at(0) // "a"
'𠮷'.at(0) // "𠮷"
````
###  includes() / startsWith() /endsWith()
 > 这三个方法都支持第二个参数，表示开始搜索的位置。
 
````
var s = 'Hello world!';
s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
````

### repeat(num) 
num会被取整

````
'na'.repeat(NaN) // ''
'na'.repeat(2.9) // 'na' 
	

````

### 自动补全 padStart() / padEnd()

````
'x'.padStart(4, 'ab') // 'abax'
'x'.padEnd(5, 'ab')   // 'xabab'
````
### 模板字符串(单行/多行)

````
console.log(`string text line 1
string text line 2`);
````

## Number

### Number.isNaN()
将全局方法parseInt(),parseFloat()移植到Number对象上面
Number.parseInt(), Number.parseFloat()

### Number.isInteger()
用来判断一个值是否为整数

> 在 JavaScript 内部，整数和浮点数是同样的储存方法，所以3和3.0被视为同一个值

````
Number.isInteger(25) // true
Number.isInteger(25.0) // true
````


### Number.EPSILON
一个极小的常量


### Math.trunc()
用于去除一个数的小数部分，返回整数部分

````
Math.trunc(4.9) // 4
Math.trunc(-4.1) // -4
Math.trunc(-0.1234) // -0
````


### Math.sign()
用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值

- 参数为正数，返回+1
- 参数为负数，返回-1
- 参数为0，返回0
- 参数为-0，返回-0
- 其他值，返回NaN



### 一个指数运算符（**）

````
2 ** 2 // 4
2 ** 3 // 8
````

指数运算符可以与等号结合，形成一个新的赋值运算符（**=）

````
let a = 1.5;
a **= 2; // 等同于 a = a * a;

let b = 4;
b **= 3; // 等同于 b = b * b * b;
````


