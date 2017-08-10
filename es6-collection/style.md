- 使用`let`替换`var`，优先使用`const`

 > JavaScript 编译器会对const进行优化  
 
 - 所有的函数都应该设置为常量(const)
 - 如果函数有多个返回值，优先使用对象的结构赋值，而不是数组的结构赋值

	````
	function nameFn() {
	  // bad
	  return [first, second, third]
	
	  //good
	  return {first, second, third}
	}
	````

- 静态化对象，添加新的属性，使用`Object.assign()`

	````
	const a = 
	Object.assign(a, { x: 3 })
	````


- 添加动态属性

	````
	const obj = {
	  id: 5,
	  name: 'San Francisco',
	  [getKey('enabled')]: true,
	};
	````

- 使用扩展运算符（...）拷贝数组，Array.form()将类似数组的数据转成数据
- 使用ESLint [使用](http://jscs.info/)
- 使用export取代module.exports

	> 只有一个输出使用`export default`
	> `export default`与普通的`export`不要同时使用
	> 输出一个函数首字母小写，输出对象首字母大写
	
	````
	module.exports 
	````


