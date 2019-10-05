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

## get传值获取方法

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

