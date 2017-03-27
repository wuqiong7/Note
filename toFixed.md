# toFixed()详解
语法

````
numObj.toFixed(digits)

````

digits: 介于 **0 到 20**，超出或没有传入直接默认为 0,
位数不够的拿 0 凑


返回：指定**小数位数的字符串**




### 直接toFixed返回结果不准问题

chrome下四舍五入不准，所以通常做法是**转换为整数再处理**避免浮点数精度的损失



````javascript
1.35.toFixed(1) // 1.4 正确

1.335.toFixed(2) // 1.33  错误
(1.335*100).toFixed()/100 //正确 1.34

1.335.toFixed(3) // 1.333  错误
(1.3335*1000).toFixed()/1000 //正确 1.34

````

### 对数字的字面量的调用

对数字的字面量直接调用会报错，
原因: .toFixed中的`.`号被解释为小数点，
fix: 字面量后加个空格调用，或者使用两个点号调用该方法。


* 数字后边加空格
* 数字后边加两个点号
* 数字加()


````javascript
756.toFixed()     // 报错 SyntaxError: Unexpected token ILLEGAL

756..toFixed()    // "756"
756 .toFixed()    // "756"
(756)..toFixed()  // "756"

````
### 带小数点


````javascript
3.14.toFixed()    // "3"
3.14 .toFixed()   // "3"
3.14..toFixed()   // SyntaxError: Unexpected token .
````

### 字面量负数
操作符优先级，**字面量负数直接调用方法不会返回字符串**

````javascript
-3.14.toFixed()   // -3  
````
