## java 两大数据类型

基本数据类型

byte

short

int

long

float

double

char

boolean

引用数据类型





#####   常见命名约定

小驼峰方法： 方法、变量   例如：firstName

大驼峰命名法：类    例如： Student ，GoodStudent

### 自动类型转换

把一个表示数据范围小的数值或者变量赋值給另一个表示数据范围

byte -----》 short ----》 int ----》 long ---》 float ----》 double

char ---》int ---》 long ---》 float ---》 double

### 强制类型转换

int k = （int）88.88    // 强制类型转换会丢失数据



### java 错误

ArrayIndexOutOfBoundsException  索引编号写错了

## 注解

```java
@Component
@ConfigurationProperties(prefix = "emp")   // 获取配置文件中的初始化数据

```

```
@Value("${emp.last-name}")   // 注入单个
```

### 创建一个控制器

```java

@Controller
public class EmpController {

    @Value("${emp.last-name}")
    public  String  name;

    @ResponseBody
    @RequestMapping("/say")
    public String sayHemmow() {
        return "sya hellow"+ name;
    }
}

```



###  加载局部配置文件

```java
@PropertySource(value = {"classpath:emp.properties"})  // 加载局部配置文件 文件在resource文件夹里
@Component
@ConfigurationProperties(prefix = "emp")
```





日志注解

@Slf4j

用法

log.info("这是要打印的日志")



### 接收参数

```java
// 两种方式
// 第一种只有表单的方式  不能是json对象 只能一个一个接
public AjaxResponse savrd(@RequestParam String id,String author){ 
                                                                 
}
// 第二种 接收json对象    接收全部
public AjaxResponse saveArticle(@RequestBody Article article) {  
    log.info("saveArticle:", article);                           
    return AjaxResponse.success(article);                        
}                                                                
```

### 请求方式----两种写法

```java
// post 请求方式两种写法
// @RequestMapping(value = "/artocle", method = POST, produces = "application/json")
    @PostMapping("/artocle")
    public AjaxResponse saveArticle(@RequestBody Article article) {
        log.info("saveArticle:", article);
        return AjaxResponse.success(article);
    }
```

```java
// delete 请求方式 两种写法
//@RequestMapping(value = "/article/{id}", method = DELETE, produces = "application/json")
      @DeleteMapping("/article/{id}")
    public AjaxResponse deleteArticle (@PathVariable Long id) {
        log.info("deleteArticle", id);
       return AjaxResponse.success(id);
    }
```

```java
// PUT 请求方式 两种写法
//@RequestMapping(value = "/article/{id}", method = PUT, produces = "application/json")
    @PutMapping("/article/{id}")
    public AjaxResponse updateArticle (@PathVariable Long id, @RequestBody Article article) {
        article.setId(id);
        log.info("updateArticle:[]", article);
        return AjaxResponse.success(article);
    }
    
// GET 请求方式 两种写法
    //@RequestMapping(value = "/article/{id}", method = GET, produces = "application/json")
    @GetMapping("/article/{id}")
    public AjaxResponse getArticle (@PathVariable Long id) {
        Article article = Article.builder().id(1L).author("cccccc").content("111111111").title("t1").build();
        return AjaxResponse.success(article);

    }
```

