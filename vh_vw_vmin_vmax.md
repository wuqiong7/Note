# vh vw vmin vmax


 vw 相对于视窗的宽度

vh 相对于视窗的高度

vmin 相对于视口的**宽度或高度中较小**的那个被均分为100单位的vmin

vmax 相对于视口的**宽度或高度中较大**的那个被均分为100单位的vmax

> “视区”所指window.innerWidth/window.innerHeight大小   
> 不包含任务栏标题栏以及底部工具栏的浏览器区域大小


### 应用场景


* 可以实现等比例图形；
[高度随宽度等比例变化的四种解决方案](https://segmentfault.com/a/1190000006631310)

 > 总感觉没什么应用场景
 
* 搭档font-size实现基于vw的自动缩放式网页布局

````
h1
  font-size: 5.9vw;
h2
  font-size: 3.0vh;
p
  font-size: 2vmin;
````
* ~~解决滚动条出现页面晃动的问题~~  

> 关于浏览器出现滚动条和消失页面不滚动有了更加终极的解决方案，经过大型项目实践已经验证相当具有可行性，这里特意分享下：

````
html {
  overflow-y: scroll;
}

:root {
  overflow-y: auto;
  overflow-x: hidden;
}

:root body {
  position: absolute;
}

body {
  width: 100vw;
  overflow: hidden;
}
````