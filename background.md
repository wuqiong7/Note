### Multipls Backgrounds
一个元素上可以使用多个背景


`background-image:url(html5.jpg),url(js.jpg),url(css.jpg);
`

如果有重叠**前面的背景图会覆盖在后面的背景图之上**(html5.jpg会盖住js.jpg)




`background: color url position repeat`

#### background-color

- color name: red
- rgb: #fff

- hsl: rgba(166, 218, 220, .5)
- hsla: hsla(182, 44%, 76%, .5)
 - 色调(H)、饱和度(S)、亮度(L)
- transparent

#### background-url

- none
- url
 - http://cdn.xxx.com/img/img.png
 - 渐变(gradient)



#### background-position

第一个用于横坐标，第二个用于纵坐标。只有一个值则是横坐标，纵坐标将默认为50%。

#### background-repeat

round space **不切割重复的图片**

- round 缩放图片的大小
- space 增加重复图片之间的距离

#### background-attachment
- fix
- scroll
- local 背景图像相对于元素内容固定，也就是说当元素随元素滚动时背景图像也会跟着滚动，因为背景图像总是要跟着内容

#### background-size
- ength：写死长宽
- percentage：写死百分比
- auto：背景图像的真实大小
- cover：等比缩放 完全覆盖 **图像有可能超出容器**
- contain 图片拉伸 完全覆盖 **图像始终被包含在容器内**




#### background-origin
- padding-box
- border-box
- content-box

**注意**
background-color是从border区域（含border）开始显示背景，  
而background-image从padding区域（含padding）开始显示背景  

#### background-clip
- padding-box
- border-box
- content-box
- text

### DEMO
[DEMO](http://jsbin.com/nawinek/edit?css,output)