# node插件 安装

 ###  post 插件

```javascript
npm install body-parser
```



# node 设计

node 的 入口文件单独一个文件

操作路由的单独一个文件

操作数据的一个单独文件



# 获取异步的数据

如果需要获取一个函数中异步操作的结果 则必须通过回调函数来获取

```javascript
//异步回调示例
exports.find = function (callback) {
    fs.readFile("./db.json", function (err, data) { 
        if (err) {
            return callback(err)
        }
        callback(null, JSON.parse(data).stund)
    })
}
```

# 重定向到首页  

res.redirect('/')

# JSON 概述

JSON.parse() 方法将数据转换为 JavaScript 对象

JSON.stringify() 方法将 JavaScript 对象转换为字符串



# mongoos 数据库操作



###连接数据库

```javascript
var mongoose = require('mongoose')
mongoose.connect('mongodb://localhost/test', {useNewUrlParser: true}) 

```

### 添加数据

```javascript
var Schema = mongoose.Schema
var userSchema = new Schema({
    names: {
        type: String,
        required: true
    },
    passwords: {
        type: String,
        required: true
    },
    email: String
})
var User = mongoose.model("User", userSchema)

var admin = new User({
    names: 'admin',
    passwords:'123456',
    email:'342730241@qq.com'
})
 admin.save(function (err, ret) { 
     if (err) {
         console.log('保存失败')
     }else{
         console.log('保存成功')
     }

  })
```

###查询集合

```javascript
User.find(function(err, ret){
      if(err) {
         console.log('查询失败')
      }else{
         console.log(ret)
      }
  })
```

### 条件查询 查询的是集合

```javascript
  User.find({names: 'admin'},function (err, ret) { 
      if (err){
         console.log('查询失败')
      }else{
          console.log(ret)
      }
   })
```

### 条件查询一个不是集合

```javascript
User.findOne({names:'admin'}, function(err, ret){
    if (err) {
        console.log('查询失败')
    }else{
        console.log(ret)
    }
})
```

### 根据 id 查询

```
findById(id, [options],[callback])
```



### 删除 

```javascript
 User.remove({
     names:'admin'
 }, function (err, ret) { 
     if (err) {
        console.log('删除失败')
     }else{
        console.log('删除成功')
     }
  })
```

### 根据条件删除一个

```javascript
User.findOneAndRemove(conditions, [options],[callback])
```

### 根据 id 删除一个

```
User.findByIdAndRemove(id, [options],[callback])
```



### 根据 id更新 必须是 id

```javascript
User.findByIdAndUpdate('id',{names:"修改内容"},function (err, ret) { 
    if (err) {
        console.log('更新失败')
    }else{
        console.log('更新成功')
    }
 })
```

### 根据条件更新所有

```javascript
User.update(conditions, doc, [options],[callback])
```

### 根据条件更新一个

```javascript
User.findOneAndUpdate([conditions],[update],[options],[callback])
```

### 例子

```javascript
var mongoose = require('mongoose')
mongoose.connect('mongodb://localhost/test', {useNewUrlParser: true});

var studnen = new mongoose.Schema({
    name:{
        type: String,
        required: true
    },
    age: {
        type: Number,
        required: true
    }
})


module.exports = mongoose.model('Student', studnen)
```



# nodejs 操作 mysql

```
npm install mysql
```

[mysql-nodejs参考手册](https://www.npmjs.com/package/mysql#introduction)



# 回调地狱

Promise 英文意思 保证 承诺

```javascript
var myFirstPromise = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve("成功") //成功调用  reject("失败")  失败调用
  }, 1000)
})
//链式调用
myFirstPromise.then(function(data) {
  //返回正确的值
  return "返回的结果"
},function() {
  //返回错误的值
  
}).then(function(data){
  //这里接收的是 上面的 "返回结果" 值
})
```

 

# Path 模块

```javascript
path.basename('c:/a/b/c/index.js')
//输出 index.js
path.basename('c:/a/b/c/index.js','.js')
//输出 index.js

//输出后缀名
path.extname('c:/a/b/c/index.js')
//输出.js

//路径转换成对象
path.parse('c:/a/b/c/index')
//输出组合 输出集合如下
	root 根目录
  dir  目录
	base 文件名包含后缀名的文件名
  ext	后缀名
  name	不包含后缀名的文件
//拼接路径
path.join('c:/a','b')
//输出 c:\\a\\b

//判断路径是否是绝对路径
path.isAbsolute('/a/b/c')

```

# node 中的其它成员

node 中有两个特殊的成员

__dirname       ***动态获取***可以用来获取当前目录

__filename	***动态获取***可以用来获取当前文件目录





# nodejs 项目

```javascript

```



项目中返回错误码才是正确

例如  约定状态码err_code

```javascript
return res.status(200).json({
  err_code:1,
  message:'用户名错误!'
})
```

重定向

```javascript
res.redirect('/')
```

cookie 可以用来保存一些不太敏感的数据

但是不能用来保存用户登陆状态



### session

```javascript
//安装
npm install express-session
//使用方法
var express = require('express')
var session = require('express-session')
var app = express()

//session 必须加这行
app.use(session({
  secret: 'keyboard cat',  //设置钥匙字符串
  resave: false,
  saveUninitialized: true
}))


//添加 session 数据
req.session.foo ="添加的数据"

//获取 session 数据
req.session.foo
```



### md5

```javascript
// 安装
npm install blueimp-md5
//使用
var md5 = require("./blueimp-md5")

var hash = md5("value")
#注意事项
//为了安全必须用多个 md5 加字符串
//例如
var hashs = md5(md5("value" + 'lastsw')) 
```

中间件就是一个方法

```javascript
//处理404页面  要放到 app.js 文件的后面
app.use(function(err, req, res, next){
  
})
```





# koa 学习

```javascript
//Koa 依赖 node v7.6.0 或 ES2015及更高版本
//koa 安装 命令
npm i koa

//解决兼容 问题  高版本 js 转换成低版本js
require('babel-register');

const Koa = require('koa');
const app = new Koa();
```

express 是自带路由模块  koa 需要安装插件

```javascript
//安装 koa-router 命令
npm install koa-router

//使用方法
var Koa = require('koa');
var Router = require('koa-router');
 
var app = new Koa();
var router = new Router();
 
router.get('/', (ctx, next) => {
  // ctx.router available
});
 
app.use(router.routes()).use(router.allowedMethods());
```



async : 让方法变成异步

await :

##	get传值获取方法

```javascript
//获取传值
router.get('/logo/:', async (ctx)=>{
    console.log(ctx.query)  //获取对象 {name:1122,age:18}
    console.log(ctx.querystring) //name=1122&age=18
    console.log(ctx.request.url) //获取url
    console.log(ctx.request.query)//获取对象 {name:1122,age:18}
    console.log(ctx.request.querystring)//name=1122&age=18
})

```

## 动态路由

```javascript
//获取动态路由的返回值
router.get('/cont/:aid/:bid', async (ctx)=>{
    console.log(ctx.params)
})
```



## 中间件

next()

### 应用及中间件



```javascript
//匹配任何路由 如果不写next就不会继续往下继续匹配
//应用及中间件
app.use(async function(ctx,next){
	ctx.body="这是一个中间件"
  await next()； //当前路由匹配完成以后继续向下匹配
})
```

### 路由及中间件

```javascript

router.use('/new',async (ctx, next)=>{
	ctx.body="这是一个路由及中间件"
  await next() //当前路由匹配完成以后继续向下匹配
})

router.use('/new',async (ctx)=>{
	ctx.body="这是一个路由及中间件" 
})
```

### 错误处理中间件

```javascript
//放在最后
app.use(async (ctx,next)=>{
  next()
  if (ctx.status ==404) {
    	ctx.status = 404
    	ctx.body="这是一个404页面"
    }
})
```



## 安装ejs模板引擎

```shell
npm i ejs
```

```
npm install koa-views 
```

###使用方法

```javascript
//引入
var views = require('keo-views')
//配置中间件
//方法1
app.use(views('views',{map:{html:'ejs'}})) //这种配置是以html结尾模板

//方法2
app.use(views('views',{extension:'ejs'})) //这种配置是以ejs结尾模板
//两种方法选一个

//渲染 使用方式
router.get('/', async (ctx)=>{
  //异步必须加await
  await ctx.render('index',{
    title:'这是渲染'
  })
})

//在模板里用法
<h1><%=title%></h1>
```

### ejs模板数据循环

```javascript
//渲染 使用方式
router.get('/', async (ctx)=>{
  let arr = ['11','222','333','444']
  //异步必须加await
  await ctx.render('index',{
    title:arr
  })
})
```

```html
<!--模板循环-->
<ul>
  <% for( var i=0;i<title.lenth;i++) { %>
  <li><%=title[i]%></li>
  <%}%>
</ul>
```

引入公共文件

```
<% include 模板路径%>  //路径不要加引号
```

解析html标签用 "-"

```javascript
//渲染 使用方式
router.get('/', async (ctx)=>{
  let arr = "<h2>这是一个h2标签<h2>"
  //异步必须加await
  await ctx.render('index',{
    title:arr
  })
})
```

```javascript
<% -title %> //解析html标签
```

条件判断

```
<%if(){%>

<%}else{%>

<%}%>
```

公共数据 放在中间件里面

```javascript
//渲染 使用方式
app.use(async (ctx, next)=>{
  ctx.state.longd="这是数据" //任何页面都可以调用到
  await next()
})
```

## post数据

```
//安装
npm i kao-bodyparser
```

接收post提交的数据

```javascript
var Koa = require('koa');
var bodyParser = require('koa-bodyparser');//引入
var app = new Koa();
app.use(bodyParser());//配置中间件
router.post('/doAdd', async (ctx)=>{
	//使用
 console.log(ctx.request.body) //会转成对象
})
```



## koa静态资源

```
//安装
npm i koa-static
```

```javascript
//使用方法
const static = require('koa-static');
const Koa = require('koa');
const app = new Koa(); 

//静态资源地址可以有多个
app.use(static(__dirname+ '/static')); //static 是静态文件夹
app.use(static(__dirname+ '/images'));//图片静态资源地址
```

## koa使用art-template

```
//安装
npm i art-template
npm i koa-art-template
```

使用方法

```javascript
const Koa = require('koa')
const render = require('koa-art-template')
const path = require('path')
const app = new Koa()
render(app, {
  root: path.join(__dirname, 'view'),//模板存放的目录
  extname: '.html', //配置模板后缀
  debug: process.env.NODE_ENV !== 'production' //是否开启调试
})

app.use(async function (ctx) {
  await ctx.render('user')
});
```

## cookie

设置cookie

```javascript
ctx.cookies.set(name, value, [options])
//[options]选项
//maxAge 一个数字表示从 Date.now() 得到的毫秒数
//signed cookie 签名值
//expires cookie 过期的 Date
//path cookie 路径, 默认是'/'
//domain cookie 域名
//secure 安全 cookie
//httpOnly 服务器可访问 cookie, 默认是 true
ctx.cookies.set("name", "这是设置的cookie", {
	maxAge：60 * 1000 * 60, //一个小时 (一般只设置这个就可以)
  path：'/news', /**配置可以访问的页面**/
  domain: '', /**正常情况下不要设置 默认是当前域名下所有页面都可以访问**/
  httpOnly:true /**true表示这个cookie只有服务器端可以访问 false 只有客户端（js）才可以访问**/
  
})
```

获取cookie

```javascript
ctx.cookies.get(name, [options])
```

## cookie 汉字转换成base64 和base64 转换汉字

cookie中文转bese64 

```javascript
//把汉字转换成base64
var userInfo = new Buffer("张三").toString('base64')
ctx.cookies.set("userInfo", userInfo))

//把base64转换成汉字
var data = ctx.cookies.get(userInfo)
var sju = new Buffer(data, 'base64').toString()
```



## session 

### session简介

  session是另一种记录客户状态的机制，不同的是Cookie保存在客户端浏览器中，而session保存在服务器上 ，session 比cookie 更安全

###安装session

```
npm i koa-session
```

###使用方法

```javascript
const session = require('koa-session');
const Koa = require('koa');
const app = new Koa();
app.keys = ['some secret hurr'];//cookie签名
const CONFIG = {
  key: 'koa:sess', /** (string) cookie key (default is koa:sess) */ 
  maxAge: 86400000,/**过期时间 【需要修稿】**/
  autoCommit: true, /**  */
  overwrite: true, /** 没有效果 默认*/
  httpOnly: true, /** (boolean) httpOnly or not (default true) */
  signed: true, /**签名 默认 */
  rolling: false, /**每次请求都强制设置cookie  默认*/
  renew: true, /** 默认(是false改成true)  当它快过期的时候就重新请求【需要修改】*/
};

//中间件
app.use(session(CONFIG, app));

//设置session
ctx.session.username= "张三"

//获取session
ctx.session.username
```



## mongodb 使用

#### 安装

```
npm install mongodb
```

#### 连接数据库 添加数据

```javascript
const MongoClient = require('mongodb').MongoClient;
// 数据库 url
const url = 'mongodb://localhost:27017';
// Database Name 数据库名字
const dbName = 'test';

MongoClient.connect(url, function(err, client) {
  const db = client.db(dbName); //连接数据库
  //添加
  db.collection("操作的表").insertOne({'id':'1','name':'张三','age':'19'}, function(err,result){
    if (!err) {
      console.log('数据增加成功')
    }
  })
  
  client.close();// 关闭数据库
})
```

#### 查询数据

```javascript
const MongoClient = require('mongodb').MongoClient;
// 数据库 url
const url = 'mongodb://localhost:27017';
// Database Name 数据库名字
const dbName = 'test';

MongoClient.connect(url, function(err, client) {
  const db = client.db(dbName); //连接数据库
  //添加
  var result = db.collection("查询的表").find({})
  result.toArray((err, docs)=>{
    	console.log(docs)//输出数据集合
  })
  
  client.close();// 关闭数据库
})
```

## mongodb 重新封装





## javascript 测试时间

```javascript
console.time('state') //测试执行时间开始
console.timeEnd('state') //测试时间结束
```

