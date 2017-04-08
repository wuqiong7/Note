# NPM包管理
* 有什么用
* 怎么用
 * [package.json](#package.json)
 * [NPM版本管理](#NPM版本管理)
 * [NPM常用命令](#NPM常用命令)
 * [发布你的NPM包](#发布你的NPM包)

## 简单介绍NPM
 NPM === node.js package management

### package.json

**必填项：名称、版本、入口文件, 许可证**

````

{
  "name": "oner-flexbox",
  "version": "1.0.0",
  "description": "oner-flexbox 是一个flex布局的小样式库",
  "main": "flexbox.css",
  "author": "gnosaij",
  "files": [
    "flexbox.css",
     "README.md"
  ],
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/oner-team/oner-flexbox.git"
  },
  "keywords": [
    "flexbox",
    "layout"
  ],
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/oner-team/oner-flexbox/issues"
  },
  "homepage": "https://github.com/oner-team/oner-flexbox#readme",
  dependencies:{},
  devDependencies:{}
}
````
[View natty-fetch's json](https://github.com/jias/natty-fetch/blob/master/package.json)




### NPM版本管理
#### 隐性约定

````
version: a.b.c
````

- a: 主版本号
 - 不向后兼容
- b: 次要版本
 - 添加向后兼容的方法
- c: 补丁版本
 - 修复向后兼容的bugs

#### 常规使用
* 指定版本

````
"oner-flexbox": "1.0.0"
````

* 波浪符+指定版本

````
"oner-flexbox": "~1.0.0"
````
> ~1.2.3 := >=1.2.3 <1.(2+1).0 := >=1.2.3 <1.3.0


* 脱字符+指定版本

````
"oner-flexbox": "^1.0.0"
````
> ^1.2.3 := >=1.2.3 <2.0.0


* 最新版本

````
"oner-flexbox": "latest"
"oner-flexbox": "*"
````




### NPM常用命令

````
npm init // 交互模式  (引导用户创建package.json，包含项目名称(必填)、版本(必填)、作者、git仓库地址)

npm set init-author-name 'Your name'
npm set init-author-email 'Your email'
npm set init-author-url 'http://yourdomain.com'
npm set init-license 'MIT'

````
````
npm init -y // 非交互模式

npm install

npm i // 缩写

npm uninstall express

npm update express


````

#### 全局(-g)

任意目录下

````
npm install express -g

npm uninstall express -g

npm update express -g

````

#### 同步package.json文件

安装/卸载的同时，添加/删除package.json中dependencies/devDependencies对应的字段

````
npm install express --save // -S

npm uninstall express --save-dev // -D

npm install express --save-exact
````

#### check项目依赖模块是否有跟新
````
npm outdated
````

#### 查看版本

````
// latest
npm view underscore version`

// all
npm view underscore versions

````


## 发布你的NPM包

#### publish
- 在npmjs.com上注册账号。[[registered]](https://www.npmjs.com/login)

-  `npm login`

	- Username
	- Password
	- Email
- ...coding....

-  `npm publish`
 > publish前，确认线上是否有重名的

#### update
##### 发正式版
- ...coding....
- 看情况 升版本

	> npm version patch <=> c++
	> 
	> npm version minor <=> b++ && c=0
	> 
	> npm version major <=> a+= && b=0 && c=0
	
-  `npm publish`

##### 发布beta(测试版本)
- ...coding....
- `npm version prerelease`
- `npm publish --tag -beta`

#### cover(不推荐)
````
npm publish --force
````

#### remove(不推荐)
````
npm unpublished 
````



#### 私有源配置

- 统一配置

````
vi $HOME/.zshrc

````

````
alias shu="npm --registry=http://npm.dtwave-inc.com:8080"

````

````
source $HOME/.zshrc // 让命令生效
````

````
shu login
shu publish
````
