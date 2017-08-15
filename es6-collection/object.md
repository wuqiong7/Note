## ES6笔记(Object)


### Object.is()

比较两个值是否相等

相等运算符（==）和严格相等运算符（===）  
缺点： **一是+0不等于-0，二是NaN等于自身**

````
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
````


### Object.assign()

`Object.assign(target, source1, source2)`

该方法实行的是浅拷贝，深拷贝的合并可用Lodash的`_.defaultsDeep`方法


undefined和null无法转成对象

- 如果它们作为首位参数，会报错
- 如果他们是非首位参数，则达到`无视`效果

  ````
  let obj = {a: 1};
  Object.assign(obj, undefined) === obj // true
  Object.assign(obj, null) === obj // true
  ````

如果参数是其他类型的值（即数值、字符串和布尔值）  
只有字符串会以数组的形式被合入target  
> 参数首先会转成对象，如果无法转成对象，就会跳过



使用场景

- 给对象添加属性、方法
- 合并、对象克隆
- **为对象指定默认值**


### Null 传导运算符(?.)

````
// 如果 a 是 null 或 undefined, 返回 undefined
// 否则返回 a.b.c().d
a?.b.c().d
````

### __proto__属性，Object.setPrototypeOf()，Object.getPrototypeOf()

用来读取或设置当前对象的prototype对象。


### Object.keys()，Object.values()，Object.entries()


#### Object.getOwnPropertyDescriptor

该方法可以获取某个对象该属性的描述对象

````
var obj = { p: 'a' };

Object.getOwnPropertyDescriptor(obj, 'p')
// Object { value: "a",
//   writable: true,
//   enumerable: true,
//   configurable: true
// }
````
