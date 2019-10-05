## 安装模板引擎

```javascript
npm install art-template -S
```

引入模板引擎

```javascript
require("art-template")
```

读取文件 fs模块

```javascript
var fs = require('fs')
fs.readFile('读取文件名字',function(err, data){

})
```

网页中静态资源处理

```javascript
if (url.indexOf('/style/') === 0) {
        fs.readFile('.' + url, function(err, data) {
            console.log('.' + url)
            if (err) {
                return res.end('404 Not')
            }
            res.end(data)
        })
```

url 核心模块 parse 拆分url路径 默认第二个参数是false

```JavaScript
url.parse(url路径,false)
```

跳转

```javascript
res.statusCode=302
res.setHeader('Location','/')
```

导出模块

```JavaScript
exports.a = add
//或者
module.exports = add
```

模块加载是优先从缓存加载



npm 常用命令

npm init

   npm init -y 跳过向导 快速生成

npm install 包名 --save   简写 npm i 包名 -S

npm uninstall 包名  如果有依赖依然会保存

npm uninstall --save 包名  删除的同时删除依赖

简写 npm un -S 包名

npm help 查看使用帮助



## npm 背墙问题

安装淘宝的 cnpm

```shell
#查看 npm 配置信息
npm config list
```

## 文件操作

文件操作都是异步的 readFile()

```javascript
//第二个参数是设置编码
fs.readFile('./db.json','utf-8', function (err, data) { 
        if (err) {
            return res.status(500).send('Server err')
        }

     })
```



## node代码修改后自动重启

```shell
npm install -g nodemon #全局安装 --globle
```

 nodemon   app.js   启动程序

查看是否安装成功

```javascript
nodemon --version
```

## express 框架

```javascript
var app = express（）
#相当于用 http.createServer()
```

```javascript
var express = require('express')
var app = express()
app.get('/', function(req, res){
    res.send('hellow express')
})
app.listen(8080, function () { 
    console.log('服务器启动成功')
 })
```

```javascript
#公共目录
app.use('/public', express.static('./public/'))
```

### express 结合art-template 安装包

```shell
npm install --save art-template
npm install --save express-art-template
```

### 配置使用art-template 模板引擎

```javascript
app.engine('html', require('express-art-template'));
```

Express为 requonse 相应对象提供了一个方法 ： render

render 方法，默认是不可以使用，但是如果配置了模板引擎就可以使用了

```javascript
res.render('html模板名'，{模板数据})
```

第一个参数不能写路径 默认会去项目中的 views 目录找查该模板文件

### 如果要修改默认的 views目录 

```javascript
app.set('views','指定目录')
```

### express 封装了重定向方法

```javascript
res.redirect('/')
```

### express 接收get数据

```javascript
//express内置了一个api 直接用
app.get('/get', function(req, res){
    var data = req.query //只能获取get数据
})
```



### express 接收post数据

```shell
##要第三方插件才能接收post数据
## 安装命令
npm install body-parser
```

```javascript
//引入包
var bodyParser = require('body-parser')
//使用包
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())
```



```javascript
app.post('/post', function(req, res){
   var data = req.body  //获取提交的post数据
})
```

### 字符串转数组 字符串转数组

```javascript
JSON.parse() //字符串转数组 

JSON.StringFy() //字符串转数组
```

### ES6 find方法

```javascript
//当某个遍历项符合item.id == data.id 条件的时候 find会终止遍历 同时返回遍历数据
data.find(function(item){
    return item.id === data.id
})
```

# node插件 安装

### post 插件

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

 

