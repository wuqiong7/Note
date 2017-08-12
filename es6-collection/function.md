## ES6笔记(function)

### 函数参数的默认值
如果传入undefined，将触发该参数等于默认值，null则没有这个效果。



### rest 参数
形式为: **...变量名**  
rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

````
const sortNumbers = (...numbers) => numbers.sort();

````


### 函数的 length 属性

指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数。
也就是说，指定了默认值后，length属性将失真

````
(function (a) {}).length // 1
(function (a = 5) {}).length // 0
(function (a, b, c = 5) {}).length // 2
(function(...args) {}).length // 0

````