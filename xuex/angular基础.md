### nvm配置

nvm是管理node的版本

[下载地址](https://github.com/coreybutler/nvm-windows/releases)

##### 有4个版本

1. nvm-noinstall.zip： 这个是绿色免安装版本，但是使用之前需要配置
2. nvm-setup.zip：这是一个安装包，下载之后点击安装，无需配置就可以使用，方便。
3. Source code(zip)：zip压缩的源码
4. Sourc code(tar.gz)：tar.gz的源码，一般用于*nix系统

##### 修改settings.txt

在你安装的目录下找到settings.txt文件，打开后加上 
node_mirror: https://npm.taobao.org/mirrors/node/ 

npm_mirror: https://npm.taobao.org/mirrors/npm/

 这一步主要是将npm镜像改为淘宝的镜像，可以提高下载速度。

##### 设置环境变量

然后我们就需要添加环境变量了：（其实只需要将root和path的路径添加到环境变量中即可）



```shell
//查看安装的node包
nvm list
//查看可安装的版本
nvm list available
//安装版本
nvm install (5.6.0)
//切换版本
nvm use 5.6.0
//删除指定版本的node
nvm uninstall 5.6.0

```



### bower 

web应用程序依赖项目管理工具

安装:

```
npm install -g bower
```

搜索包地址 <https://bower.io/search/>

### Gulp

自动完成一系列重复性的操作

网站地址 <https://gulpjs.com/>

安装

```
npm install gulp-cli -g
npm install gulp -D
```

如果安装有问题就安装淘宝镜像地址

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

在根目录下建立 gulpfile.js 文件

在gulpfile文件中写入

```
var gulp = require('gulp');
gulp.task('say', function(){
    console.log('hello word')
})
```

一个目录拷贝到另一个目录里

```
gulp.task('copy', function(){ 
    gulp.watch("src/index.html",async ()=>{
        gulp.src("src/index.html") .pipe(gulp.dest("C:\\Users\\Administrator\\Desktop\\angular\\dist"));
    })
})
```

安装less 解析less

```JavaScript
var less  = require('gulp-less')
var path = require('path');
gulp.task('styles', function () { 
    return gulp.src('src/styles/demo.less')
    .pipe(less({
        paths: [ path.join(__dirname, 'less', 'includes') ]
      }))
    .pipe(gulp.dest('C:\\Users\\Administrator\\Desktop\\angular\\dist\\style'))
 })
```

创建本地服务器

```
npm install gulp-connect --save
```

合并文件

```
npm install gulp-concat --save
```

最小化js文件

```
npm install gulp-uglify --save
```

重命名文件

```
npm install gulp-rename --save
```

最小化css

```
npm install gulp-minify-css --save
```

压缩html文件

```
npm install --save gulp-htmlmin
```

最小化图像

```
npm install gulp-imagemin --save
```



### 自动刷新

Browsersync + Gulp.js 

```
//启动一个服务器  自动刷新
npm install browser-sync gulp --save-dev
```

```
var gulp        = require('gulp');
var browserSync = require('browser-sync').create();

// Static server
gulp.task('browser-sync', function() {
    browserSync.init({
        server: {
            baseDir: "./"
        }
    });
});
```

--save-dev  安装早devDependencies 开发依赖

devDependencies -D

例如 npm install gulp -D   安装到devDependencies  开发依赖里

dependencies  -S 

例如  npm install jquery -S    安装到 dependencies   项目依赖里

```
npm install -D babel-core babel-preset-es2015 babel-preset-stage-1 browser-sync cross-env del gulp gulp-autoprefixer gulp-babel gulp-cache gulp-changed gulp-clean-css gulp-concat gulp-eslint gulp-htmlmin gulp-imagemin gulp-md5-assets gulp-sass gulp-uglify run-sequence
```

 



## JavaScript 作用域

```JavaScript
;(function () { 
   console.log('这是里面一层内容');
 })()

 !function () {  
     console.log('11111111111111111111')
 }()

 +function () { 
    console.log('22222222222222')
  }()
```

## git操作

```shell
git init    //初始化一个本地的仓库
git status  //查看本地仓库的状态
git status -s  //输出简要的日志
git add .    //添加到跟踪列表
git commit -m "说明"   //提交到本地仓库
git diff   //对比差异
git log    //查看日志
git reset --hard 版本的后6位   //回退到某个版本
```

.gitignore   忽略文件



# angular

angular 1.4  叫angularjs

angular4 叫 angular

#### 安装angularcli

```
npm install -g @angular/cli

ng version   //查看安装的信息

ng  new auction  //创建项目
```

#### 

![](angular\20190607224135.png)



####  安装jquery 要安装类型描述文件



```
npm install jquery --save
npm install bootstrap --save
npm install @types/jquery --save-dev
npm install @types/bootstrap --save-dev
```

####  创建组件

```
ng g component 创建的目录
例如
ng g component components/home
```



### 路由  Route

```JavaScript
//在app-routing.model.ts 中定义路由
const routes: Routes = [
  {path: '', component: HomeComponent},
  {path: 'product', component: ProductComponent},
  {path: '**', component: Code404Component} //如果输入的路由不存在就跳这个路由
];
```

```html
 //在html中使用
<a [routerLink]="['/']">主页</a>
<a [routerLink]="['/product']">商品详情</a>
<router-outlet></router-outlet>
```

### 按钮跳转

在模板里写

```html
<input type="button" value="跳转商品详情" (click)="getusresd()">
```

```JavaScript
import { Component } from '@angular/core';
import { Router} from "@angular/router"; //倒入路由模块

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'router-demo';
  constructor (private router: Router){//获取路由
      
  }
  getusresd(){//点击按钮时跳转路由
    this.router.navigate(['product'])
    //this.router.navigate(['product','2'])//传递参数 
  }

}
```

### 在路由时传递数据有三种

在查询参数中传递数据

在路由路径中传递数据

在路由配置中传递数据

```
//传递参数
<a [routerLink]="['/product']" [queryParams]="{id: 1}">商品详情</a>
```

![](angular\QQ截图20190608154213.png)

```javascript

//路由参数获取
import { Component, OnInit } from '@angular/core';
import {ActivatedRoute} from "@angular/router";

@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrls: ['./product.component.css']
})
export class ProductComponent implements OnInit {

  private productId:number;//定义接收参数的变量
  constructor(private routerInfo: ActivatedRoute) {

  }
  ngOnInit() {
    this.productId = this.routerInfo.snapshot.queryParams['id'] //获得传递过来的参数
  }

}

```

![](angular\QQ截图20190608154735.png)



两种传递参数

第一种

```html
<!--html-->
<a [routerLink]="['/product']" [queryParams]="{id: 1}">商品详情</a>
```

```JavaScript
<!---->
private productId:number;
constructor(private routerInfo: ActivatedRoute) {
  }
  ngOnInit() {
    this.producUrlId = this.routerInfo.snapshot.params['id']
  }
```



```JavaScript
//在路由中定义
{path: 'product', component: ProductComponent},
```

第二种

```html
<!--html-->
<a [routerLink]="['/product','1']">商品详情</a>
```

```javascript
private  producUrlId:number;
constructor(private routerInfo: ActivatedRoute) {
  }  
ngOnInit() {
    this.routerInfo.params.subscribe((params:  Params) => this.producUrlId = params['id']); //这样定义是没有缓存的
    
   //this.producUrlId = this.routerInfo.snapshot.params['id']
    //snapshot 参数快照  有缓存
  }
```

```JavaScript
//在路由中定义
{path: 'product/:id', component: ProductComponent},
```



### 路由重定向

```
//访问 跳转到 home中
{path: '', redirectTo: '/home', pathMatch:'full'},
```



### 子路由

```JavaScript
const routes: Routes = [
  {path: '', redirectTo: '/home', pathMatch:'full'},
  {path: 'home', component: HomeComponent},
  //添加子路由
  {path: 'product/:id', component: ProductComponent,children: [
      {path: '', component: ProductDescComponent},
      {path: 'seller/:id', component: SellerInfoComponent}
    ]},
  {path: '**', component: Code404Component}
];
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

```html
//在父级页面中加入
<a [routerLink]="['./']">商品描述</a>
<a [routerLink]="['./seller',9]">销售员信息</a>
<router-outlet></router-outlet>
```



### 辅助路由

```html
<a [routerLink]="[{outlets: {aux: 'chat'}}]">开始聊天</a>
<a [routerLink]="[{outlets: {aux: null}}]">结束聊天</a>
//跳转到路由里
<a [routerLink]="[{outlets: {primary:"home",aux: 'chat'}}]">结束聊天</a>
<router-outlet nam="aux"></router-outlet>
```

```
//app-routing.module.ts
{path: 'chat', component: ChatComponent, outlet: "aux"},
```



### 路由守卫

只有当用户已登录并拥有某些权限时才能进入某些路由

一个由多个表单组件组成的向导，例如注册流程，用户只有在当前路由的组件中填写了满足要求的信息才可以导航到下一个路由。

当用户未执行保存操作而试图离开当前导航时提醒用户。

#### 三种路由守卫

CanActivate: 处理导航到某个路由的情况。

CanDeactivate ：处理从当前路由离开的情况

Resolve：在路由激活之前取路由数据

