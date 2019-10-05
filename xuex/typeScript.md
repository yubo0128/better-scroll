## typeScript中的数据类型

布尔类型(boolean)

var falg:boolean = true;

数字类型(number)

字符串类型(string)

数组类型(array)

```typescript
//两种定义方式
var arr:number[] =[1,2,3,4,5]

var arr:Array<number>=[1,2,3,4,5]
```

元组类型(tuple)

//为每个数组指定类型 元组类型

var arr[number,string] = [123,'元组']

枚举类型(enum)

enum sex {男=1,女=2} 

任意类型(any)

null 和undefined

void 类型

```typescript
//定义方法   表示方法没有任何返回类型
function run():vode{ 
  console.log('run')
}
//如果有返回值  有什么类型的返回值就写什么类型
function numb():number{
  return 1234
} 
```

never 类型  其他类型



typescript 增加的类型校验

写ts代码必须指定类型

```typescript
//一个元素可以设置多个类型
var num: number | null | undefined;
```

