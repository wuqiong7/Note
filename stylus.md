# Stylus

keyframes什么鬼

Sass 和 Stylus 更进一步，分别用 @at-root 和 / 符号作为嵌套时「根」规则集的选择器引用。这有什么用呢？举个例子，

-----

### 嵌套

> / 符号作为嵌套时「根」规则集的选择器引用
 
````
.clsName
  .module
    width:90%;
    .module-title
      font-size:12px
      /.clsName .module-active
        color:red;

等价于:

.clsName
  .module
    width:90%;
    .module-title
      font-size:12px
  .module-active
    color:red;
	    
```` 

### 混入模式
类似于Less也可以一层套一层

````
***Less:***
.levle1(){
  font-size:12px;
}
.levle2(){
  .levle1;
  color:red;
}
body{
 .levle2
}

***Stylus:***
levle1()
  font-size:12px;
levle2()
  levle1()
  color: red;
body
 levle2()
````

#### 将声明块作为混入参数
````
方式一：
red(foo)
  color: red
  {foo}

.alert
  foo =
    font-weight: 700
    font-size: 1.5em
  red(foo)
  
方式二：
// 用关键词 block 输出的方式。要传入声明块的 mixin 前添加 + 符号

red()
  color: red
  {block}

.alert
  +red()
    font-weight: 700
    font-size: 1.5em
  
````

### 选择器
换行和逗号同等效果  
**有这么个提示，但尚未发现例外的**
> 该规则唯一的例外就是长得像属性的选择器。

### CSS字面量
````
@css{
  // 这里放css
}
````

### @import
`@import "fileName"`  
后缀名不写默认`.styl`

支持类似js的引用  
`@import “module”` 可被解析为`@import "module.styl"`或者是`@import "module/index.styl"`


> Less 在字符串中进行插值：

````
@device: mobile;
@import "styles.@{device}.css";
````

> Stylus 字符串拼接的插值：

````
device = "mobile"
@import "styles." + device + ".css"
````



### @extend
Stylus: 只要选择器匹配，就可以生效  
Less: 默认只继承父类本身的样式，如果要同时继承嵌套定义在父类作用域下的样式，得使用关键字 all
> [Less文档](http://lesscss.org/features/#extend-feature-extend-all-)   :extend (.clsName all) 

**继承会影响CSS输出的顺序**

### 变量
**在Stylus中不要使用“@”符号开头声明变量**
> 使用"@"符号开头来声明（0.22.4）变量，Stylus会进行编译，但其对应的值并不会赋值给变量。  
> Less是必须以@开头

````
@width = 2px;
.clsName
 width:@width;
 height:10px;
 
输出: 
@width = 2px;
.clsName {
  width: ;
  height: 10px;
}

````

正确姿势：

````
$font-size = 12px;         // 1. 常规用法

min()
  font-size: $font-size;
  width:20px;
  padding: (@width/2);     // 2. 块属性访问
  height: h=20px;   
  margin-top: (h/2);      // 3. 变量放在属性中
  
````

#### 属性查找
“向上冒泡”原则，若没有则返回null，编译时会报错

#### 为属性设置默认值

`z-index: 1 unless @z-index`

#### 变量作用域
> Less 更倾向接近 CSS 的声明式，计算过程弱化调用时机；  
> Sass 和 Stylus 更倾向于指令式

````
Stylus:
size = 10px
.box
  width: size

size = 20px
.ball
  width: size
    
输出：
.box {
  width: 10px;
}
.ball {
  width: 20px;
}

**************************
Less:

@size: 10px;
.box {
    width: @size;
}

@size: 20px;
.ball {
    width: @size;
}

输出：
.box {
  width: 20px;
}
.ball {
  width: 20px;

````  


### Tips

#### 变量

**上边变量模块里方法2、方法3中使用时必须用`()`抱起来，不然会报错**

> Stylus中/当作为属性使用的时候需要用括号括起来

````
body
  font 14px/1.4
  font (14px/1.4)
  
生成的代码:

body {
  font: 14px/1.4;
  font: 10px;
}
````

#### 父级引用（&）不做省略
在继承`@extend .clsa > input`下边第一种写法会报错。

````
// 能运行,但不推荐
.clsa
  > input
    color: red
    
// 建议写法
.clsa
  & > input
    color: red
````

#### for循环前边必须有空格

````
table
  for i in (1...5)
    th:nth-child(i)
      height: 10px * i
````



### nibStylus插件(使用Autoprefixer、PostCSS替换)

> 它们强制我们使用新的语法。它们迭代慢于现代浏览器，所以当稳定版发布时会产生很多不必要的前缀，有时我们需要创建自己的mixins。


### 方法(看看了解思路即可)

````
// position简写

-pos(type, args)
  i = 0
  position: unquote(type)
  {args[i]}: args[i + 1] is a 'unit' ? args[i += 1] : 0;
  {args[i += 1]}: args[i + 1] is a 'unit' ? args[i += 1] : 0;

absolute()
  -pos('absolute', arguments)

fixed()
  -pos('fixed', arguments)



// 属性类似，抽成List

apply(props)
  props = arguments if length(arguments) > 1
  for prop in props
    {prop[0]} prop[1]

body
   apply(width 1px, height 2px, padding 3px)
body
 list = (width 1px)(height 2px)(padding 3px)
 apply(list)



// 加前缀一:用Function传参实现(推荐)

vendor(prop, args)
  -webkit-{prop} args
  -moz-{prop} args
  {prop} args

border-radius()
  vendor('border-radius', arguments)

box-shadow()
  vendor('box-shadow', arguments)

button
  border-radius 1px 2px / 3px 4px


// 加前缀二
// 此处if里用`===`会报错

vendors = webkit moz o ms official
border-radius()
 for vendor in vendors
   if vendor == vendors
      border-radius: arguments
   else
      -{vendor}-border-radius: arguments
````

## 推荐阅读
* [Stylus官网](http://stylus-lang.com/)
* [stylus中文版参-张鑫旭](http://www.zhangxinxu.com/jq/stylus/)
* [再谈 CSS 预处理器](http://efe.baidu.com/blog/revisiting-css-preprocessors/)
