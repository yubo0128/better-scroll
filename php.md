```php
$a =1;
unset($a);  //删除变量
isset($a) ;//判断变量是否存在
```

### php有八种数据类型

##### 四种标量

布尔型（boolean）

整型（integer）

浮点型（float）

字符串（String）

##### 两种复合类型

数组（array）

对象（Object）

##### 两种特殊类型

资源（Resource）

Null



3. 实例化：new从一个抽象的概念得到一个符合抽象

概念的具体实例的过程

4. 类成员：member 

指类class结构中的所有内容，类成员里有三种

5. 方法：method 

本质是在class构造中创建的函数也称之为成员方法或

者成员函数

6. 属性：property 

本质是在类class构造中创建的变量，也称之为成员变

量

7. 类常量：constant 

本质是在类class结构中创建的常量



### 面向对象

1. 类 class 是定义面向对象主体的最外层结构用来包裹主体的数据和功能（函数）类是一类具有共性事务带表，代表的是事务的共性。
2. 对象:object 是某类事务的具体代表，也是实际数据和功能操作的具体单元，也被称之为实例
3. 实例化：new从一个抽象的概念得到一个符合抽象概念的具体实例的过程
4. 类成员：member 指类class结构中的所有内容，类成员里有三种
5. 方法：method 本质是在class构造中创建的函数也称之为成员方法或者成员函数
6. 属性：property 本质是在类class构造中创建的变量，也称之为成员变量
7. 类常量：constant 本质是在类class结构中创建的常量

 

php中类成员有三种 

成员变量（属性）

成员方法（成员函数）

类常量

```php
//{}是类结构
class name{}
```

```php
class Nothing{
 public $name=1; //成员变量 或者属性
}
$name = new Nothing();//对象保存在队区
echo $name->name;//访问成员变量
$name->name='这是成员变量'; //修改成员变量
echo $name->name;
$name->age = 10; //添加成员变量
echo $name->age;
echo "<hr>";
//unset($name->age);//删除成员变量
//echo $name->age;
```

#### 返回当前类名

```php
class Nmas{
    function displ(){
        echo __CLASS__; //返回当前的类名
    }
}

$ad = new Nmas();
$ad->displ();
```

#### 定义常量 类里只能用 Const定义

```php
class Fff{
    const PI = 3.1446;
}
```

#### 访问修饰限定符

public   公有

protected  受保护的

private	私有的



#### 构造方法

__construct()

```php
class Ring{
    public function __construct(){
       echo __CLASS__;
    }    
}
$e = new Ring();
```

#### 析构方法

```
class Sale{
   public function __destruct(){
        //销毁对象所占用的资源代码
   }
}
```

#### 对象传值

```
class Sa{}

$s1 = new Sa();
$s2 = $s1;  //引用对象
```

#### 类常量访问   :: （范围解析操作符）

```php
class Saler{
   const PI = 13.2;//定义常量
}
$e = new Saler();
echo Saler::PI; //访问常量
```



#### 静态成员

1. 静态属性：在类中定义属性的时候使用static 关键字修饰 访问的时候只能使用类+范围解析操作符+静态属性访问

```php
class Saler{
	public $m = 0;
	public static $c = 0; //静态属性
}
//静态属性访问
echo Saler::$c;
```

2. 静态方法

```php
class Saler{
	 public static function show(){
	    return 1;
	 }
}
//类直接访问
Saler::show()
```



#### self 关键字

1. self 是用来代替类名的

```php
class Ring{
    const PI = 13.2;
    public function __construct(){
        echo __CLASS__;
    }
    public static function name(){
        return self::PI;
    }    
}
echo Ring::name();
```

#### 自动加载类 php7不推荐用 __autoload

```php
//自动加载
function __autoload($classname){
    echo $classname;//返回的值是 Saler 
	include_once $classname.'php';
}
$s = new Saler()

    
    
// 自动加载多个文件 
function __autoload($classname){
    echo $classname;//返回的值是 Saler 
    $c_flie = "c/".$classname.'.class.php'; 
    if(file_exists($c_flie)){
        include_once $c_flie;
        exit;
    }
    $f_flie= "m/".$classname.'.class.php'; 
    if(file_exists($f_flie)){
        include_once $f_flie;
        exit;
    }
}

$s = new Saler()

```

##### php 7自动加载用 spl_autoload_register()

```php
function my_autoload($classname){
    echo $classname;//返回的值是 Saler 
    $c_flie = "c/".$classname.'.class.php'; 
    if(file_exists($c_flie)){
        include_once $c_flie;
        exit;
    }
    $f_flie= "m/".$classname.'.class.php'; 
    if(file_exists($f_flie)){
        include_once $f_flie;
        exit;
    }
}

spl_autoload_register('my_autoload'); //php7 注册

$s = new Saler()
```

用类的方法写自动加载

![](php\QQ截图20190526211655.png)



#### 对象克隆

```php
class Saler{
	public $name;    
 public function __clone(){ //克隆时执行这个方法
     var_dump($this); 
 }
}

$s1 = new Saler();
// 克隆出来后是两个对象 不一样的对象
$s2 = clone $s1;


```

```php
class Saler{
	public $name;
    //克隆私有化 外部不能执行
     private function __clone(){ //克隆时执行这个方法
         var_dump($this); 
     }
}

$s1 = new Saler();
// 克隆出来后是两个对象 不一样的对象 定义了私有化就不能被克隆
$s2 = clone $s1;

```

### 设计模式

#### 单列模式

​	类最多只有一个对象称之为单列



#### 工厂模式





###  面向对象三大特性

##### 封装



##### 继承 

extends  

php 中继承是子类继承父类所有的公有成员、受保护的和私有属性 、不能继承父类的私有方法

private   （子类都不能访问）

protected（不能在类外部访问 只能在类内部访问）

##### 多态

php中不支持多态    php不是强制类型

