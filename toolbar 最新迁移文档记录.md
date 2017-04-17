
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


#### ToolBar  控制 返回键的颜色及大小

```

<style name="toolbar_theme" parent="@style/ThemeOverlay.AppCompat.Dark.ActionBar">  
        <item name="colorControlNormal">@color/color_text_black</item>  
        <item name="android:actionBarSize">46dp</item>  
</style>  
```

```
<style name="toolbar_blue_theme" parent="@style/ThemeOverlay.AppCompat.Dark.ActionBar">  
        <item name="colorControlNormal">@color/color_text_blue</item>  
        <item name="android:actionBarSize">46dp</item>  
</style> 
```
colorControlNormal就是我们指定的返回键的颜色，Android：actionBarSize 是我们可以另指定的Toolbar高度

[](http://img.blog.csdn.net/20160503150845033?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
[](http://img.blog.csdn.net/20160503151113942?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)












