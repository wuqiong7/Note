# Flexbox

## 目录
* [Flexbox相关属性](#属性)
 * 盒模型计算规则(padding/margin/box-sizing) 
* [margin:auto与Flexbox的巧妙结合](#margin:auto与Flexbox的巧妙结合)
* [DEMO](#DEMO)
* [相关阅读](#相关阅读)

## 属性
* flex
* display
* flex-direction
* justify-content
* align-items
* align-self
* align-content
* flex-wrap
* order

### flex(划重点啦!)
`flex: none | <' flex-grow '> <' flex-shrink >'? || <' flex-basis '>`

**flex-grow在「flex」属性中该值如果被省略则默认为「1」,单独使用时默认值为0**



剩余空间 = Flexbox width - flex item width总和(各item的flex-basis总和)

剩余空间 > 0  ？ 扩张flex-grow : 收缩flex-shrink


#### 计算(flex-grow)

````
<ul class="flex">
    <li>a</li>
    <li>b</li>
    <li>c</li>
</ul>

.flex{display:flex;width:600px;margin:0;padding:0;list-style:none;}
.flex li:nth-child(1){width:200px;}
.flex li:nth-child(2){flex-grow:1;width:50px;}
.flex li:nth-child(3){flex-grow:3;width:50px;}
````
> 本例中b,c两项都显式的定义了flex-grow，flex容器的剩余空间分成了4份，其中b占1份，c占3分，即1:3
> 
> flex容器的剩余空间长度为：600-200-50-50=300px，所以最终a,b,c的长度分别为：
> 
> a: 50+(300/4)=200px
> 
> b: 50+(300/4*1)=125px
> 
> a: 50+(300/4*3)=275px


#### 计算(flex-shrink)
````
<ul class="flex">
    <li>a</li>
    <li>b</li>
    <li>c</li>
</ul>
.flex{display:flex;width:800px;margin:0;padding:0;list-style:none;}
.flex :nth-child(1){flex:1 1 300px;}
.flex :nth-child(2){flex:2 2 200px;}
.flex :nth-child(3){flex:3 3 400px;}
````

> 本例定义了父容器宽（即主轴宽）为800px，由于子元素设置了伸缩基准值flex-basis，相加300+200+400=900，那么子元素将会溢出900-800=100px；
> 
> 由于同时设置了收缩因子，所以加权综合可得300*1+200*2+400*3=1900px；

> 于是我们可以计算a,b,c将被移除的溢出量是多少：
> 
> a被移除溢出量：(300x1/1900)x100，即约等于16px
> 
> b被移除溢出量：(200x2/1900)x100，即约等于21px
> 
> c被移除溢出量：(400x3/1900)x100，即约等于63px
> 
> 最后a,b,c的实际宽度分别为：300-16=284px, 200-21=179px, 400-63=337px



#### 符合属性缩写

*「flex: 1」=== 「1 1 0%」

*「flex: auto」===「1 1 auto」

*「flex: none」===「0 0 auto」

*「flex」初始值:「flex: 0 auto」或者「flex: initial」===「0 1 auto」
 
#### flex Tips
* flex-grow时，flex-item设置了max-width,则以max-width准，不再做放大。
 * all item都设置了max-width，加起来还不够Flexbox的宽度，则多余的就留白
* flex-shirnk时候, flex-item设置了min-width，则以min-width准，不再做缩
小处理。
 * all item都设置了min-width,加了起来已经超过了Flexbox的宽度，则直接溢出
* 同时设置flex-basis和width，width属性会被覆盖
 * 如果flex-basis和width其中有一个是auto，那么另外一个非auto的属性优先级会更高。 
* flex-basis和width为auto值，那最后的空间就是根据内容多少来定的，内容多占据的水平空间就多。

#### 单独使用
flex-grow: 默认值0
 
flex-shrink: 默认值1
 
flex-basis: 默认值auto


### display
`display: flex | inline-flex`

一旦给容器设置了`display:flex;`或`display:inline-flex;`,需要注意的点：

* Flexbox 不支持 ::first-line 和 ::first-letter 这两种伪元素
 
* vertical-align对其子元素无效

* float和clear对其子元素无效，也不会使子元素脱离文档流(**但是对Flexbox是有效果**)

* 多栏布局（column-*） 在 Flexbox 中也是失效的，就是说我们不能使用多栏布局在Flexbox 排列其下的子元素（鱼和熊掌不可得兼嘛）

* 其子元素不会继承父级容器的宽

### flex-direction
`row | row-reverse | column | column-reverse`

### justify-content
`flex-start | flex-end | center| space-between | space-around`

* space-between：平均分配，左边与主轴起始位置对其，右边与主轴结束位置对其
* space-around：平均分配，间距是平均分配

### align-items
`align-items: flex-start | flex-end | center| stretch | baseline`

* stretch: 内容撑开铺满Flexbox容器
* baseline: 以所有内容元素的基线作为对齐标准

### align-self
`align-self: flex-start | flex-end | center| stretch | baseline`

与align-items相同，用于个性化子元素的样式重写。

**注意：并没有justify-seft这东西，因为完全可以用margin auto实现**

### align-content
`align-content: flex-start | flex-end | center| stretch`

与align-items类似。多上处理所以就没有`baseline`   
只是align-items是针对单行的。而align-content是针对多行的处理

### flex-wrap
`flex-wrap: no-wrap | wrap | wrap-reverse`

### order
`order: <integer>`

默认值0  
数值小的排在前面。可以为负值


## margin:auto与Flexbox的巧妙结合
### Tips
* `margin:auto`仅针对当前的flex item，对其子元素无效。
* 在flex计算中flex-bases与flexible lengths （main size与cross size）时，auto margins取值为0
* `margin:auto`优先级 > `justify-content`与`align-self`

 > 如剩余空间为正数，则剩余空间会被平均分配在相应方向上auto margin(s)的flex元素之间
 
 > 如剩余空间为负数，则将主轴方向的auto margin(s)设定为‘0’。

* `margin:auto`对溢出的（overflowing）flex item无效

## DEMO
* [戳这里调试demo(Flexbox)](http://jsbin.com/gogabiv/edit?css,output)

* [戳这里调试demo(margin:auto布局Flexbox)](http://jsbin.com/kuxino/1/edit)

## 相关阅读
* [CSS参考手册](http://www.css88.com/book/css/properties/flex/flex.htm) 
* [深入解析CSS Flexbox](http://www.jianshu.com/p/ee3b2b45d85d)

* FlexBox弹性盒子计算
 * [FlexBox弹性盒子计算规则](https://segmentfault.com/a/1190000005006056)
 * [带padding or box-sizing弹性盒子的相关计算](http://stackoverflow.com/questions/34753491/how-does-flex-shrink-factor-in-padding-and-border-box)  
 * [深入理解 flex 布局以及计算](https://www.w3cplus.com/css3/flexbox-layout-and-calculation.html)
* margin:auto与Flexbox的巧妙结合
 * [flex与margin结合做布局](http://www.voyax.me/2016/07/19/%E5%A6%82%E4%BD%95%E6%8E%A7%E5%88%B6flex%20item%E5%9C%A8%E4%B8%BB%E8%BD%B4%E4%B8%8A%E7%9A%84%E5%B8%83%E5%B1%80/)
 * [margin:auto与flexbox的巧妙结合](http://www.jianshu.com/p/beeb93a76830)