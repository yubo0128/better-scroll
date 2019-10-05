### php验证方式为正整数

```php
 
 protected function insnummber($value){
                    //参数依次为验证数据，验证规则，全部数据（数组），字段名
        //这里我们要判断的验证的数据要求必须为正整型
        if(is_numeric($value) && is_int($value+0) && ($value+0) > 0){
            return true;
         }else{
            //如果不符合我们的条件，返回错误信息，在控制器中可以用getError()方法输出
            return $'不是整型';
         }
    }
```

