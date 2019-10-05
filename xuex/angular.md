angular 安装cli脚手架

```shell
npm install -g @angular/cli
ng new my-dream-app  //创建项目
//运行项目
cd my-dream-app
ng server --open 
```

## 文件介绍

browserslist 是支持浏览器的配置文件



### 创建组件

```
ng g component 创建的目录
例如
ng g component components/home
```

```javascript

@NgModule({
  /**  配置的组件 */
  declarations: [
    AppComponent,
    HomeComponent,
    HeaderComponent
  ],
  imports: [ /** 配置当前模块运行依赖的其它模块 */
    BrowserModule,
    AppRoutingModule
  ],
  providers: [], /** 配置项目所需要的服务器 */
  bootstrap: [AppComponent] /** 指定应用的主视图 */
})
```

### 声明属性的几种方式

public    公共(默认)

protected  保护类型

private    私有的



## 数据

```javascript
//第一种
public title = '我是数据';

//第二种
msg = '我也是数据';
//第三种 字符串类型
username:String = '张三';
//第四种 any 是任意类型 推荐 数据类型不清楚可以用 any
public studenr:any = '我是数据'

public userinfo:object = {
  name:'zs',
  age:18
}
```

## 指令

### 模板数据绑定

```html
<div [title]="msg">我是绑定title的数据</div>
```

### 解析html代码

```javascript
public msg = "<h4>这是解析标签</h4>"

<div [innerHTML]="msg"></div>
```

### 渲染数组

```javascript
//定义数组方法一
public arr =['111','2222','3333','4444']
//定义数组方法二 推荐用这种
public list:any[] = ['11','222','333']

//在模板里使用方式
<li *ngFor="let item of arr">
	{{item}}
</li>


---------------------------------------------------------

public items: Array<string> = ['是字符串', '是字符串2'];

public items: Array<any> = ['是任意类型', '是任意类型2'];
```

### 循环数组里的对象

```javascript
public items: any[] = [
{name:'测试1',age:21},
{name:'测试2',age:22},
{name:'测试3',age:23},
{name:'测试4',age:24},
{name:'测试5',age:25}
]
 
//在模板里使用方式
<li *ngFor="let item of items">
	{{item.name}} {{item.age}}
</li>
```

### 获取数据循环的索引

```javascript
//在模板里使用方式
<li *ngFor="let item of items;let key = index">
	{{item.name}} {{item.age}} {{key}}
</li>
```

### 判断

```javascript
public flag:boolean = true;

//模板用法
<div *ngIf='flag'>
		显示文字
</div>

//没有else只有*ngIf


```

### ngSwitch判断

```javascript
<ul [ngSwitch]="数据名称">
	<il *ngSwitch="2">显示</li>
</ul>
```

### 条件判断语句 [ngClass] [ngStyle]

```html
//设置class
<div [ngClass]='{'red':msg==true}'>
   ngClass
</div>
```

```
public arrr = red;
<p [ngStyle]="{'color': arrr}">我是ngStyle</p>
```

### 自定义管道

```
public datasd: any = new Date();

<p>{{datasd | date:'yyy-MM-dd HH:mm ss'}}</p>
```

### 事件

```
<p (click)='run()'>事件</p>

run(){
  console.log('事件')
}

<button (keydown)="rem($event)">点击</button>
<button (keyup)="rem($event)">点击</button>
```



### 双向数据绑定

双向数据绑定只针对表单 只有表单才生效

```
//引入模块 在app.module.ts里
import { FormsModule } from '@angular/forms'

在imports里加入  FormsModule

<input name="" value="" [(ngModel)]="keywods">
<p>{{keywods}}</p>
```

### 表单

结合双向数据绑定

```typescript
public peopInfo: any = {
    username: '',
    sex: '1',
    citys: ['北京', '上海', '深圳'],
    city: '深圳',
    hobby: [{
      title: '吃饭',
      checked: false
    }, {
      title: '睡觉',
      checked: false
    }, {
      title: '打游戏',
      checked: true
    }],
    mark: ''
  };
```



```html
<ul>
    <li>姓名<input type="text" value="" name="username" [(ngModel)]="peopInfo.username"></li>
    <li>姓名<input type="radio" value="1" name="sex" [(ngModel)]="peopInfo.sex">男<input type="radio" name="sex" [(ngModel)]="peopInfo.sex" value="2">女</li>
    <li>姓名
      <select name="" id="" [(ngModel)]="peopInfo.city">
        <option [value]="item" *ngFor="let item of peopInfo.citys">{{ item }}</option>
      </select>
    </li>
    <li>姓名
      <span *ngFor="let item of peopInfo.hobby; let key=index;">
        <input type="checkbox" name="" [id]="'check'+key" [(ngModel)]="item.checked"><label [for]="'check'+key">{{item.title}}</label>
      </span>
    </li>
    <li>
      <textarea name="" [(ngModel)]="peopInfo.mark" id="" cols="30" rows="10"></textarea>
    </li>
  </ul>
```







