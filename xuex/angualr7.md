### 属性声明

string 字符串

any  任意类型

```
public student:any = "我是一个学生“
```

绑定数据

```
<div >
  {{name}}
</div>
```

绑定属性

```
<div  [title]="name"></div>
```

绑定模板

```
<div [innerHtml]="conterm"></div>
```



##### 定义数组的三种方式

```typescript
public  asad = ['1211','2222','3333'];
public list:any[] = ['222','3333','4444','5555'];
public  items:Array<any> = ['数组1','数组2','数组3','数组4'];
```

示例1

```
public user:any[]=[
    {id:1,'name':'张三'},
    {id:2,'name':'李四'},
    {id:3,'name':'王五'}
]
```

```html
<ul>
<li *ngFor="let cint of user">{{cint.id}} ---- {{cint.name}}</li>
</ul>

<!--key-->
<ul>
  <li *ngFor="let item of user;let i =index">{{item}}-----{{i}}</li>
</ul>

```

### ngIf

```html
<li *ngIf="!flag">这是判断</li>
```



### ngSwitch

```HTML
<span [ngSwitch]="">
    <p *ngSwitchCase="true">

    </p>
    <p *ngSwitchCase="false">

    </p>
    <p *ngSwitchDefault>

    </p>
</span>
```

### ngClass

```
<li [ngClass]="{'color':true}"></li>
<li [ngClass]="{'color':false}"></li>

```

### ngStyle

```
<li [ngStyle]="{'color':'red'}"></li>

```

###  常用的管道（pipe）有

<http://bbs.itying.com/topic/5bf519657e9f5911d41f2a34>

angular中的管道(pipe)是用来对输入的数据进行处理，如大小写转换、数值和日期格式化等。

**angular中的管道(pipe) 以及自定义管道适用于angular4 angualr5 angualr6 angular7**

常用的管道（pipe）有

#### 大小写转换

```
<p>{{str | uppercase}}</p>//转换成大写
<p>{{str | lowercase}}</p>//转换成小写
```

#### 日期格式转换

```
<p>{{today | date:'yyyy-MM-dd HH:mm:ss' }}</p> 
```

####  小数位数

//接收的参数格式为{最少整数位数}.{最少小数位数}-{最多小数位数} //保留2~4位小数

```
<p>{{p | number:'1.2-4'}}</p> 
```

#### JavaScript 对象序列化

```
<p>{{ { name: 'semlinker' } | json }}</p> 
<!-- Output: { "name": "semlinker" } -->
```

#### slice 字符串截取

```html
<p>{{ 'semlinker' | slice:0:3 }}</p> <!-- Output: sem -->
```

#### 管道链

```html
<p>{{ 'semlinker' | slice:0:3 | uppercase }}</p> <!-- Output: SEM -->
```

#### 把数据转换成json

```
public ssa:any={
  usmeName:'111',
  age:22
}
//在页面上使用
<pre>
{{ ssa | json }}
</pre>
```



#### 表单keydown事件

```
<input type="text" name="" id="" (keydown)="soe($event)">

soe(e){
  console.log(e.target.value);
  console.log("111")
}
```

#### 获取事件对象

```
<button (click)="renEvent($event)">执行方法获取事件对象</button>

renEvent(e){
	var dom:any = event.target;
	dom.style.css.color="red";
}
```

#### 双向数据绑定 只是针对表单

在 app.module里引入

```
import { FormsModule} from "@angular/forms";
```

在impoets里声明使用FormsModule

```
imports: [
  BrowserModule,
  AppRoutingModule,
  FormsModule
],
```

```
<input type="text" value="" [(ngModel)]="keywoded">
<p>{{keywoded}}</p>

public keywoded:any = '这是默认值';
```

##### 双向数据绑定

```html
<ul>
  <li>姓名:<input type="text" value="" placeholder="" [(ngModel)]="arsd.user"></li>
  <li>性别:
    <input type="radio" name="sex" value="1" checked id="sex1"  [(ngModel)]="arsd.sex"/><label for="sex1">男</label>
    <input type="radio" name="sex" value="0" id="sex2" [(ngModel)]="arsd.sex"/> <label for="sex2">女</label></li>
  <li>姓名:<input type="text" value="" placeholder="" [(ngModel)]="arsd.age"></li>
  <li>居住城市：
    <select name="" [(ngModel)]="arsd.city">
      <option *ngFor="let item of arsd.cityList">{{item}}</option>
    </select>
  </li>
  <li>
    爱好：
    <span *ngFor="let item of arsd.hobby;let key = index">
      <input type="checkbox" name="" [id]="'check'+key" [(ngModel)]="item.checkde"><label [for]="'check'+key">{{item.title}}</label>
    </span>
  </li>
  <li>
    备注:
    <textarea [(ngModel)]="arsd.bodys"></textarea>
  </li>
  </ul>
```

```typescript
public arsd:any = {
  user:'1221',
  sex:'1',
  cityList:['重庆','北京','上海','广州','成都','贵州','沈阳'],
  city:"上海",
  hobby:[{title:'吃饭',checkde:false},
         {title:'睡觉',checkde:false},
         {title:'打豆豆',checkde:false}],
  bodys:'这是测试数据'
}
```

#### 创建服务  服务是放公共的方法

创建服务命令

```
ng g service my-new-service
//创建到指定目录下面
ng g service service/storage
```

在app.module.ts 里引入服务和配置服务

```
import { StorageService} from "./services/storage.service"; providers: [StorageService],//配置服务
```

在使用的地方引入

```typeScript
import {StorageService} from "../../services/storage.service";
//使用
constructor(public storage:StorageService) {
    let s= this.storage.get();
    console.log(s);
  }
```

#### ngOnInit

```typescript
//生命周期函数 组件和指令初始化完成，并不是真正的dom加载完成
ngOnInit(){

}
//视图加载完成以后触发的方法
ngAfterContentInit(): void {
  }
```

#### ViewChild

```html
<div #mybox>
  我是amgasdasd
</div>
```

```typescript
import { ViewChild} from '@angular/core';
@ViewChild("mybox",{static: true}) myBox:any; //angualr8
@ViewChild("mybox") myBox:any; //angualr7
//生命周期函数
ngAfterContentInit(): void {
    console.log(this.myBox.nativeElement.style.color="red");
    console.log(this.myBox.nativeElement.innerHTML)
  }
```

可以调用或执行子组件的方法和数据

```
//父组件引入子组件
<app-footer #foot></app-footer>
```

```
//在父组件里
import {ViewChild} from '@angular/core';
 @ViewChild("foot") foot:any;
 ngAfterContentInit(): void {
    console.log(this.foot.gock())//子组件的方法

  }
```



#### **父组件给子组件传值**

@input

值和方法都可以传递

```
//在父组件定义
public title:string ="我是父组件传过来的值";
//父组件的的方法
run(){
console.log('这是父组件的方法');
}
//在子组件上传
<app-footer #foot [title]="title" [run]="run"></app-footer>
```

```
// 在子组件里接收
import {Input} from '@angular/core';
 @Input() title:any;
 @Input() run:any;//接收方法
 //执行父组件的方法
 runds(){
 	this.run() 
 }
//在子组件输出
<div>{{title}}</div>
<div (click)="runds()">执行父组件的方法</div>
```

可以把父组件所有的内容都传递到子组件

```
//在父组件中
<app-footer [home]="this"></app-footer>
```

```
//在子组件中接收父组件的所有方法
import {Input} from '@angular/core';
 @Input() home:any;
 
 //可以执行父组件的所有方法和属性
 this.home.run()
  this.home.title
```

#### 子组件给父组件传值

方法一

​		ViewChild 可以获取子组件的方法和数据

方法二

Output

EventEmitter

```

```



#### 非父子组件传值

服务可以通讯

```
services
```

### 异步 Rxjs

```

```

