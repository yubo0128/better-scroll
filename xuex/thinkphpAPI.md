插件 <https://www.kancloud.cn/he_he/thinkphp5/981160>

## 路由

两种方式定义路由 

配置试路由

```php
  '__pattern__' => [
        'name' => '\w+',
    ],
    '[hello]'     => [
        ':id'   => ['index/hello', ['method' => 'get'], ['id' => '\d+']],
        ':name' => ['index/hello', ['method' => 'post']],
    ],
```

动态注册路由

```php
use think\Route;
//get方式请求          https方式请求
Route::rule('hellpo','index/index/hellow','GET',['https'=true]);
//支持get也支持post
Route::rule('hellpo','index/index/hellow','GET|POST');

Route::get('hellpo','index/index/hellow')
Route::post('hellpo','index/index/hellow')
   // any 支持 * 星号
Route::any('hellpo','index/index/hellow')
```

```php
Route::rule('路由表达式','路由地址','请求类型','路由参数(数组)','变量规则（数组）');
```

### URL路由模式

1、PATH_INFO

2、混合模式

3、强制使用路由模式

配置文件

```
// 是否开启路由
    'url_route_on'           => true,
// 是否强制使用路由
    'url_route_must'         => false,  //默认是关闭的
```

### php请求类型 安全性 和幂等性

```
//5这种
GET     ：查询
POST    ：创建
DELETE	：删除
PUT			：更新
*
```

| 方法名  | 安全性 | 幂等性 |
| ------- | ------ | ------ |
| GET     | 是     | 是     |
| HEAD    | 是     | 是     |
| OPTIONS | 是     | 是     |
| DELETE  | 否     | 是     |
| PUT     | 否     | 是     |
| POST    | 否     | 否     |

### 传掺数

```
Route::get('hellpo/:id','index/index/hellow')
```

### 获取参数 三种方法

第一种

```php
  public function hellow($id){
        echo $id;
    }
```

第二种

```php
use think\Request;

//获取单个     //不区分http请求类型的param()
$id = Request::instance()->param('id')   
$name = Request::instance()->param('name')
 //一次性获取所有的传的参数
 $all = Request::instance()->param()
     var_dump($all)
     
 //获取问号后面的参数的请求方法
  //http://think.vide/hellpo?id=1123
 $id = Request::instance()->get()
 
//获取路径的参数
//http://think.vide/hellpo/1123
 $id = Request::instance()->route()
     
//获取post参数
 $id = Request::instance()->post()
```

### tp5 接收参数助手函数

```php
//获取所有的
$all = input('param');
//获取单个
$all = input('param.id');

$all = input('get')
$all = input('get.id')

$all = input('post')
$all = input('post.id')
```

### 依赖注入获取参数

```php
    public function hellow(Request $request){
        $all = $request->param();
        var_dump($all);
    }
```



### 版本定义

![](php\QQ截图20190509214030.png)

```php
//路由配置
use think\Route;
Route::get('banner/:id','api/v1.Banner/getBanner');
```



### 参数校验

***两种用法***    独立验证和验证器  验证器有优势减少代码量 更好的封装

**独立验证**

内置验证规则  <https://www.kancloud.cn/manual/thinkphp5/129356>

```php
 $data = [
      'name' => "vendoasdasasdadsad",
       'email' => "342730241@qq.com"
   ];
 $validate = new Validate([
        'name' => 'require|max:10',
         'emali' => 'email'
     ]);
```

```php
//只是执行单个验证
$result = $validate->check($data);
//有错输出错误
echo $validate->getError();
```

```php
//执行批量验证
$rsd = $validate->batch()->check($data);
//批量验证是数组
var_dump($validate->getError())
```

**验证器**

![](php\QQ截图20190509221932.png)

```php
//controller里
$data = [
    'name' => "vendoasdasasdadsad",
    'email' => "342730241qq.com"
  ];
 $validata = new TestValidate();
 $result = $validata->batch()->check($data);
 var_dump($validata->getError());
```

```php
//Validate 里
namespace app\api\validate;
use think\Validate;
class TestValidate extends Validate
{
    // protected $rule = []  //必须这样写
    //规定好的
    protected $rule = [
        'name' => 'require|max:10',
        'email' => 'email'
    ];
}
```

#### 验证器例子

```php
namespace app\api\validata;
class bannerId extends IDEgetbanner
{
    protected $rule =[
        'id' => 'require|insnummber'
    ];
    protected function insnummber($value,$rule="",$data="",$field=""){
                    //参数依次为验证数据，验证规则，全部数据（数组），字段名
        //这里我们要判断的验证的数据要求必须为正整型
        if(is_numeric($value) && is_int($value+0) && ($value+0) > 0){
            return true;
         }else{
            //如果不符合我们的条件，返回错误信息，在控制器中可以用getError()方法输出
            return $field.'不是整型';
         }
    }
}
```



### 返回错误信息

```php
throw new Exception($error);
```



### RESTFul API 

  参考豆瓣开放API

  非常标准的API   GitHub 开发者API

### 设置全局异常处理

   单个错误抛出

```php
try{
    $banner = BannerModel::getBannerById($id);
}catch (Exception $ex){
    $err = [
       'error_code' => 10001,
        "msg"=>'error'
    ]; 
  //返回错误信息   返回400状态码
    return json($err, 400);
}
return $banner;
```

