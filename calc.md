# calc()

**注意：用空白符把 - 和 + 隔起来，否则会产生解析错误！**
> 表达式中有“+”和“-”时，其前后必须要有空，乘除也建议尽量有空格


[兼容性](http://caniuse.com/#feat=calc)

## 支持写法

````
width: calc(10% + 20%); => width: 30%;
width: calc(150px * 2); => width: 300px;
width: calc(150px + 50px); => width: 200px;
width: calc(1000px - 2px); => width: 998px;
````


## 常规应用场景

* panel布局

 除去head部分，剩下撑满。 ==> [戳这里看calc()完美实现品字布局](http://jsbin.com/welotug/edit?html,css,output)
 
````
width: calc(100% - 50px);
````
  

* background-position

一个为之宽度的容器做背景固定在右下角，然后力右边缘和底部分别都有个20px的距离。
	
````
background-image: url(url.png);
background-position: calc(100%-20px, 100%-20px);
````
	
* 左右布局，37占比，中间有个10px的间距
	
````
.sidebar
  float: left;
  width: 30%;
  margin-right: 10px;
.main
  float: right;
  width: calc(70% - 10px);
````
	
* 栅格计算

````
.column-1-7 
  width: calc(100% / 7);
.column-2-7
  width: calc(100% / 7 * 2);
.column-3-7
  width: calc(100% / 7 * 3);
````
	
* 变相设置box-sizing
 
````
.module
  padding: 10px;
  
  /* Same as box-sizing: padding-box */
  width: calc(40% - 20px);
  border: 2px solid black;
	
  /* Same as box-sizing: border-box */
  width: calc(40% - 20px - 4px);
````