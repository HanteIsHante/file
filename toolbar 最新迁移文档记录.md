
# [ToolBar](https://developer.android.com/reference/android/widget/Toolbar.html)




### android中怎样去掉标题栏

> 在代码里实现

```
this.requestWindowFeature(Window.FEATURE_NO_TITLE);//去掉标题栏  
```

PS：这句代码要写在setContentView()前面。

> 在样式文件（style.xml）里面实现

```
 <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

```









