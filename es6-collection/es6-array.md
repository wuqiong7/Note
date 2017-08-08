## ES6笔记(Array)

### 扩展运算符

将一个数组转为用逗号分隔的参数序列

````
[...'hello'] // ["h", "e", "l", "l", "o"]
````

合并数组(concat)

````
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);
````

与解构赋值结合**只能放在参数的最后一位，否则会报错**

````
const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]
````

### Array.from
将类似数组的对象转为数组


### Array.of

总是返回参数值组成的数组,如果没有参数，就返回一个空数组

就避免了下代码的尴尬

````
Array() // []
Array(3) // [, , ,]
Array(3, 11, 8) // [3, 11, 8]
````

返回数组

````
Array.of() // []
Array.of(undefined) // [undefined]
Array.of(1) // [1]
Array.of(1, 2) // [1, 2]
````

### includes

可替换indexOf,且更具优势

````
[NaN].indexOf(NaN)  // -1
[NaN].includes(NaN) // true
````
> 懵逼脸 -_-
> 
> 另外，Map 和 Set 数据结构有一个has方法，需要注意与includes区分。
Map 结构的has方法，是用来查找键名的，比如Map.prototype.has(key)、WeakMap.prototype.has(key)、Reflect.has(target, propertyKey)。
Set 结构的has方法，是用来查找值的，比如Set.prototype.has(value)、WeakSet.prototype.has(value)。


### find/findIndex
 - find: true 返回**第一个**符合条件的成员 else 返回`undefined`
 - findIndex: true 返回第一个符合条件的数组成员的**位置** else 返回`-1`


````
// 这两个方法都可以发现NaN
[NaN].find(item => Object.is(NaN, item)) // NaN
[NaN].findIndex(item => Object.is(NaN, item)) // 0
````