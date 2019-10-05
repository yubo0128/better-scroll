### widget

```
import 'package:flutter/material.dart';
void main(){
runApp(MyApp())
}
```



```dart
class MyApp extends StatelessWidget{
    @overrid
    Widget build(BulidContext context){
       return Center(class MyApp extends StatelessWidget{

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title:Text(
            "title信息",
            style: TextStyle(
              fontSize: 20.0,
              color: Colors.pink
            ),
          ),
        ),
        body: HomCenter(),
      ),
      theme: ThemeData(
        primarySwatch: Colors.deepPurple
      ),
    );
  }
}
        child: Text(	
               "text这是类容",
                style: TextStyle(	
                    fontSize: 40.0,
                    color: Colors.yellow,	
                )
            )
        )
    }
}
```

## Container  和Text基本组件用法

```dart
class HomCenter extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Center(
        child: Text(
          '这是内容',
        //  textAlign: TextAlign.center,
          // overflow: TextOverflow.ellipsis,
          style: TextStyle(
              fontSize: 20.0,  //字体大小
              color: Colors.red,   // 颜色
              fontWeight: FontWeight.w400, // 加粗
              fontStyle: FontStyle.italic,  // 斜体
              decoration: TextDecoration.lineThrough, //文本线 none 没有线  lineThrough 删除线 overline 上划线  underline 下划线
              decorationColor: Colors.teal , // 线的颜色
              decorationStyle: TextDecorationStyle.wavy,// wavy 波浪线  double 两根线 solid 一根线  dashed dotted 虚线
              letterSpacing: 3.0, // 中文字间距
          ),
        ),
      ),
      width:300,  //
      height: 300,
      decoration: BoxDecoration(
        color: Colors.yellow, // 边框颜色
        border: Border.all(
          color: Colors.blue,  // 边框颜色
          width:2.0,//边框大小 边框宽度
        ),
        borderRadius: BorderRadius.all(  // 边框圆角
          Radius.circular(10)
        )
      ),
      // margin: EdgeInsets.all(10), // 内边距
      // margin: EdgeInsets.fromLTRB(left, top, right, bottom),
      // padding: EdgeInsets.all(30), // 外边距
        // padding: EdgeInsets.fromLTRB(left, top, right, bottom),
      // transform: Matrix4.translationValues(x, y, z),  // 位移
      // transform: Matrix4.rotationZ(0.3), // 旋转   z轴旋转
      // transform: Matrix4.diagonal3Values(x, y, z),  // 缩放
      // alignment: Alignment.topRight,   //位置 ??? 没效果

    );
  }
}
```

## 网络图片  

圆方法一

```dart
/**
 * 圆角图片第一种方法
 */
class HomCenter extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Container(
//        child: Image.network( // 网络图片
//          'https://cdn.jsdelivr.net/gh/flutterchina/website@1.0/images/homepage/header-illustration.png',
//          alignment: Alignment.topRight,  //图片位置
//           fit: BoxFit.cover,  // cover全屏显示相当于
//         // repeat: ImageRepeat.repeatY, // 平铺
//        ),
        width:200,
        height: 200,
        decoration: BoxDecoration(
          color: Colors.deepPurple,
//          borderRadius: BorderRadius.all(
//            Radius.circular(150)
//          ),
          borderRadius: BorderRadius.circular(20), // 圆角 和上面效果一样
          image: DecorationImage(
            image: NetworkImage('https://cdn.jsdelivr.net/gh/flutterchina/website@1.0/images/homepage/header-illustration.png'),
            fit: BoxFit.cover
          )
        ),
      ),
    );
  }
}
```

圆方法二

```dart
class HomCenter extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Container(
        child: ClipOval( // 转换成圆形图片
          child: Image.network(
           'https://cdn.jsdelivr.net/gh/flutterchina/website@1.0/images/homepage/header-illustration.png',
            width: 200,
            height: 200,
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}
```

## 本地图片 

```dart
在flueert 根目录下建立images文件夹
    在pubspec.yaml 里加上图片路径 如下
   assets:
    - images/b.png
/**
 * 本地图片
 */
class HomCenter extends StatelessWidget{

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Container(
        child: Image.asset('images/b.png'),
        height: 300,
        width: 300,
      ),
    );
  }
}
```

## flutter列表

水平列表

```dart
class HomCenter extends StatelessWidget{

  @override
  Widget build(BuildContext context) {
    return ListView(
      padding: EdgeInsets.all(20),
      children: <Widget>[
        ListTile(
        //  leading: Icon(Icons.brightness_1,color: Colors.red,), // 图标
          leading: Image.network("https://cdn.jsdelivr.net/gh/flutterchina/website@1.0/images/homepage/header-illustration.png"), // 图片
          title: Text(
              '标题标题标题',
              style: TextStyle(
                fontSize: 20
              ),
          ),
          subtitle: Text('内容内容内容内容内容内容内容'),
        ),
        ListTile(
          leading: Image.network("https://cdn.jsdelivr.net/gh/flutterchina/website@1.0/images/homepage/header-illustration.png"), // 图片
          title: Text('标题标题标题'),
          subtitle: Text('内容内容内容内容内容内容内容'),
        ),
      ],
    );
  }
```

水平列表

```dart
class HomCenter extends StatelessWidget{

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 300.0,
      child: ListView(
        scrollDirection: Axis.horizontal,  // horizontal水平  默认就是垂直列表
        children: <Widget>[
          Container(
            width: 180.0,
            height: 300.0,
            color: Colors.orange,
            child: ListView(
              children: <Widget>[
                Image.network(
                    "https://cdn.jsdelivr.net/gh/flutterchina/website@1.0/images/flutter-mark-square-100.png",
                    alignment: Alignment.center
                ),
                Text('我是文本',textAlign: TextAlign.center,)
              ],
            ),
          ),
          Container(
            width: 180.0,
            height: 180.0,
            color: Colors.blue,
          ),
          Container(
            width: 180.0,
            height: 180.0,
            color: Colors.pink,
          ),
          Container(
            width: 180.0,
            height: 180.0,
            color: Colors.tealAccent,
          ),
        ],
      ),
    );
  }
}
```

