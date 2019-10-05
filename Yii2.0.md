### 获取get参数

```php
//Url路径 http://www.yiis.com/index.php?r=index/index&id=3333

$request = \Yii::$app->request;
$aa= $request->get("id"); //获取url参数的id的值 
//设置默认参数为1  如果id没有值 就赋值为1
$aa= $request->get("id",1);
```

### 获取post

```php
$request = \Yii::$app->request;
$aa= $request->post("id"); //获取url参数的id的值 
//设置默认参数为1  如果id没有值 就赋值为1
$aa= $request->post("id",1);
```

### 判断是什么方式请求的

```php
$request = \Yii::$app->request;
$aa= $request->isGet;//判断是否为get请求的

$aa= $request->isPost;//判断是否为Post方式请求的

//获取用户的ip地址
$aa= $request->userIP;
```

### 分配数据到模板里 就两个方法

```php
// 传递数据到模板页面
return $this->renderPartial('index',['data'=>$data]);
```

```php
return $this->render('index',['data'=>$data]); //带默认头部和底部
```



#### 多数组合并一个数组

```php
$dat1 = [
'id'=>1,
'name'=>2
]
$dat2 =[
'id'=>2,
 'name'=>3
]
//多个数组合并
compact($dat1,$dat2,$dat3)

```

### 字符串过滤在模板里

```php
//先引入这个助手类
 use \yii\helpers\Html;
<h1><?php echo Html::encode($str);?></h1>
    
 // yii还提供了一个过滤的工具，能够把js等敏感代码完全过滤掉
use \yii\helpers\HtmlPurifier;
<h1><?php echo HtmlPurifier::process($str);?></h1>
```

###  自定义模板

```php
//在 views/layouts 里定义 home.php 加入 <?=$content;?>
//在controller 里定义
 Public $layout = 'home'; //定义默认公共模板
 
//模板共用 在模板里使用 在模板里调用模板
<?php
 echo $this->render("模板名称");    
?>
```

####  执行原生sql语句

```php
$sql= "select * from banner";
$rr = Banner::findBySql($sql)->all;

// 
$request = \Yii::$app->request;
$aa= $request->get("id"); //获取url参数的id的值 
//防止sql注入 这样写安全
$sql= "select * from banner where id=:id"; //id是站位符
$rr = Banner::findBySql($sql,[':id'=$aa])->all;
```



### 获取全部数据

```php
Banner::find()->all();
```

### 条件查询

```
Banner::find()->where(['id'=>6])->all();
//条件查询 5>=id >=2  查询 2和5之间的内容
Banner::find()->where(['between','id',2,5])->all();
//模糊查询
Banner::find()->where(['link','title','图像识别技术'])->all();

```

### 取一条数据

```php
Banner::find()->where(['id'=>6])->one();//
//查询一条数据更简单方法
Banner::findOne(5) //查询id等于5的    
```

### 查询多条数据简单方法

```php
Banner::findAll([2,4,5]); //查询id为 2 4 5
```

### 对象变成数组

```php
Banner::find()->asArray()->all(); //转成数组
```

### 数据多使用batch() 减少服务器压力

```php
foreach(Banner::find()->batch(2) as $artutcle){
	$data[] = $artutcle
}
var_dump($data);
```

### 添加数据

```php
$articlre= new Banner();
$articlre->name="这是添加的数据";
$data= $articlre->insert(); //方法一
$data= $articlre->save();//方法二

//取得数据的id
$articlre->attributes['id']; //获取添加的id
```

### 修改

```php
$articlre= Banner::findOne(1) //获取id为1的数据 返回对象
$articlre->name="这是修改的数据";
$articlre->update(); //返回1 修改成功   方法一

$articlre->save(); //方法二


```

### 单个字段增加

```php
//更新字段名称 +1   id 为 1    字段加1       执行条件
Banner::updateAllCounters(['字段名称'=>1],['id'=>1]);
```

### 删除

```php
$articlre= Banner::findOne(1) //获取id为1的数据 返回对象
$articlre->delete(); //删除查询出了的 id为 1 的数据  方法一

//方法二
Banner::deleteAll("id=1"); // 删除id为一的数据

//可以使用占位符
Banner::deleteAll("id=:id",[':id'=>1]);

//删除多条件
Banner::deleteAll("id>:id And name=:name",[':id'=>1,":name"=>"王五"]);

```

### 一对多关联查询

```php
$category = Catrhory::findOne(2);//查询数据库Catrhory id为2的数据
					//banner_id 是banner的        id是Catrhory的id
$category->hasMany("app\models\Banner",['banner_id'=>'id'])->all(); //方法一


$category->hasMany(Banner::className(),['banner_id'=>'id'])->all(); //方法二
```



### 一对一

```php
$articlre= Banner::findOne(1) //获取id为1的数据 返回对象
    							//	id 是Catrhory的
 $articlre->hasOne('app\models\Catrhory',['id'=>'banner_id'])->all();
```











# YII

## 资源管理组件

### 全局加载

```php
use app\assets\AppAsset;
AppAsset::register($this);

//在AppAsset 里
public $cssOptions=[
        "noscript" =>true //给css包裹一层noscript标签
    ];
    public $jsOptions=[
        'condition' => 'let IE9', //ie 9 加载
        'postiotn' =>\yii\web\View::POS_HEAD //放在顶部
 ];
```

### 按需求加载

```php

//按需求加载 js/2.js  
//"position"=> \yii\web\View::POS_HEAD  //加载的在头部
//依赖 'depends'=>"yii\web\YiiAsset"   这是默认的jq和yii
$this->registerJsFile("js/2.js",["position"=> \yii\web\View::POS_HEAD,'depends'=>"yii\web\YiiAsset"]);

//加载css
$this->registerCssFile('css/cs2.css',["depends"=>"yii\bootstrap\BootstrapAsset"])；

//在页面中执行js代码
$js=<<<JS
    console.log('this is js1')
JS;
$this->registerJs($js);

//在页面中加载css
$cc="body{baclground:red;}"
$this->registerCss($css);

```

