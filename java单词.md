# 注解

在头部注解

```java
@Slf4j    //日志
@RestController             // 返回json 的注解 json数据的响应
@RequestMapping("/rest")    // @RequestMapping 除了可以使用请求URL 映射请求外，还可以使用请求方法、请求参数及请求头映射请求



```

实体类

```java
@Data    // 给实体类加上get set tostring 方法
@AllArgsConstructor    //加这个注解不需要写构造函数
```



在函数上注解

```java
 @RequestMapping(value = "/artocle", method = POST, produces = "application/json")  //除了可以使用请求URL 映射请求外，还可以使用请求方法、请求参数及请求头映射请求
@RequestBody    //主要用来接收前端传递给后端的json字符串中的数据的(请求体中的数据的)；GET方式无请求体，所以使用@RequestBody接收数据时，前端不能使用GET方式提交数据，而是用POST方式进行提交。在后端的同一个接收方法里，@RequestBody与@RequestParam()可以同时使用，@RequestBody最多只能有一个，而@RequestParam()可以有多个。

```



# 单词

Mapping  /mæpɪŋ/ 映射，映现

