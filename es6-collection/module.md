## ES6笔记(module)


模块功能主要由两个命令构成：export和import。
export命令用于规定模块的对外接口，
import命令用于输入其他模块提供的功能。


### export

- export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系

- export可以位于代码的任何位置，只要处于模块的顶层就可以
  > 如果处于块级作用域内，就会报错，下一节的import命令也是如此。这是因为处于条件代码块之中，就没法做静态优化了，违背了ES6模块的设计初衷。

- import命令具有提升效果，会提升到整个模块的头部，首先执行。




**import是静态执行**

所以不能使用表达式和变量，这些只有在运行时才能得到结果的语法结构。

````
// 报错
import { 'f' + 'oo' } from 'my_module';

// 报错
let module = 'my_module';
import { foo } from module;

// 报错
if (x === 1) {
  import { foo } from 'module1';
} else {
  import { foo } from 'module2';
}

````


**如果多次重复执行同一句import语句，那么只会执行一次**，而不会执行多次。


````
import { foo } from 'my_module';
import { bar } from 'my_module';

// 等同于
import { foo, bar } from 'my_module';
````

通过 Babel 转码，CommonJS 模块的require命令和 ES6 模块的import命令，可以写在同一个模块里面，但是最好不要这样做。


> ES6 模块与 CommonJS 模块的两个重大差异  
> - CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。  
> - CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。  






### 模块的整体加载

````
import * as circle from './circle';

// **不允许运行时改变** 下面两行都是不允许的
circle.foo = 'hello';
circle.area = function () {};
````




### export default 命令
用export default输出的类，import时无需加`{}`


如果想在一条import语句中，同时输入默认方法和其他接口

````
import _, { each, each as forEach } from 'lodash';
````

对应上面代码的export语句如下。

````
export default function (obj) {
  // ···
}

export function each(obj, iterator, context) {
  // ···
}

export { each as forEach };
````



### import()

**引擎处理import语句是在编译时**

因为require是运行时加载模块，import命令无法取代require的动态加载功能。

````
const path = './' + fileName;
const myModual = require(path);
````
上面的语句就是动态加载，require到底加载哪一个模块，只有运行时才知道。import语句做不到这一点。


````
import('./myModule.js')
.then(({export1, export2}) => {
  // ...·
});


// import()也可以用在 async 函数之中
async function main() {
  const myModule = await import('./myModule.js');
  const {export1, export2} = await import('./myModule.js');
  const [module1, module2, module3] =
    await Promise.all([
      import('./module1.js'),
      import('./module2.js'),
      import('./module3.js'),
    ]);
}
main();
````