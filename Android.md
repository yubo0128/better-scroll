## 布局管理器

### 线性布局（LinearLayout）

   

| android:id            | android:layout_margin  |
| --------------------- | ---------------------- |
| android:layout_width  | android:layout_padding |
| android:layout_height | android:orientation    |
| android:background    |                        |



### 相对布局（RelativeLayout）

android:layout_toLeftOf

android:layout_toRightOf

android:layout_alignBottom

android:layout_alignParentBottom

android:layout_below



```java
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <view
        android:id="@+id/view_1"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="#FF5722"
        />
    <View
        android:id="@+id/view_2"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="#fff5"
        android:layout_below="@id/view_1"
        />
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="200dp"
        android:background="#ff2225"
        android:layout_below="@id/view_2"
        android:orientation="horizontal"
        android:padding="14dp"
        >
        <view
            android:layout_width="50dp"
            android:layout_height="50dp"
            android:background="#3F51B5"></view>
        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="#4CAF50"
            >
            <View
                android:id="@+id/view_3"
                android:layout_width="100dp"
                android:layout_height="match_parent"
                android:background="#00BCD4"
                />
            <View
                android:layout_width="100dp"
                android:layout_height="match_parent"
                android:background="#FF9800"
                android:layout_toRightOf="@+id/view_3"
                android:layout_marginLeft="10dp"
                />
        </RelativeLayout>
    </LinearLayout>
</RelativeLayout>
```







# 安卓单词



layout  布局；设计；安排；陈列















# 安卓学习

// 目录

res/drawable   保存图片或者是保存9Patch 图片文件

res/layout       存储安卓布局文件

res/mipmap   存储启动图标的





Android:id 属性

Android:background 属性

