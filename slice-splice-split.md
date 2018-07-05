### slice

`arrayObject.slice(start,end)`

- 返回的是一个新数组
- 含头不含未(start to end)



### splice

`arrayObject.splice(index,howmany,item1,…..,itemX)`

- 第一个，第二个参数为必填
- 第二个参数为要删除的项目数量,如果设置为 0, 则不会删除项目 

````
var replace = lang.splice(1,1,"c#","ruby"); //删除一项，插入两项 
console.log(lang);  //console.log(replace); //返回删除的项
````


### split

`String.split(“separator”)`
- 字符串分割
