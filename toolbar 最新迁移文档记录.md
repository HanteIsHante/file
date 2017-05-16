
# [ToolBar](https://developer.android.com/reference/android/widget/Toolbar.html)




## android中怎样去掉标题栏

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

> 我们创建的每一个Activity默认都是使用了ActionBar的,那么为了使用ToolBar,我们就应该首先去掉默认的ActionBar。注意我们应该去掉ActionBar,这里使用requestWindowFeature(Window.FEATURE_NO_TITLE);是不可以的,程序运行之后仍然会报错:

```
 Caused by: java.lang.IllegalStateException: This Activity already has an action bar supplied by the window decor. Do not request Window.FEATURE_SUPPORT_ACTION_BAR and set windowActionBar to false in your theme to use a Toolbar instead.                                               
```
我们这里在 res/values/styles.xml下编辑:
```
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="AppTheme.Base">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>


    <style name="AppTheme.Base" parent="Theme.AppCompat.Light">
        <item name="windowActionBar">false</item>
           <!--注意当我们使用API版本为22及以上来编译的时候要去掉前缀android:-->
        <item name="windowNoTitle">true</item>
    </style>
</resources>


```


通过上面的编辑我们就可以完成ToolBar的添加了，这也是最常用的做法。 
当然我们也可以直接将AppTheme继承自系统已有的主题也能满足效果。
```
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
    </style>

```



## ToolBar  控制 返回键的颜色及大小及 menu 菜单键的颜色

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

![toolbar_theme](http://img.blog.csdn.net/20160503150845033?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

![toolbar_blue_theme](http://img.blog.csdn.net/20160503151113942?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

同时,代码中添加 

```
setSupportActionBar(mToolbar);  
 ActionBar actionBar =  getSupportActionBar();  
        if(actionBar != null) {  
            actionBar.setDisplayHomeAsUpEnabled(true);  
            actionBar.setDisplayShowTitleEnabled(false);  
        }  
```


#####   Fragment 中添加toolbar

Fragment没有setSupportActionBar
```
        AppCompatActivity mAppCompatActivity = (AppCompatActivity) mActivity;
        Toolbar toolbar = (Toolbar) mAppCompatActivity.findViewById(R.id.toolbar);
        mAppCompatActivity.setSupportActionBar(toolbar);       
        ActionBar actionBar = mAppCompatActivity.getSupportActionBar();
        if (actionBar != null) {
              activity.getSupportActionBar().setDisplayHomeAsUpEnabled(true);
            activity.getSupportActionBar().setDisplayShowTitleEnabled(false);
        }
```







## 如何用设计师切好的图替换我们系统原生的返回键呢？方法有两个

> 1、在我们引入的Appbar的theme中添加一个Item，将设计师给我们的图放进去

 ```
<item name="android:homeAsUpIndicator">@drawable/web_detail_back</item> 

```

> 在我们的Toolbar中添加属性

```
app:navigationIcon="@drawable/web_detail_back"  
```
添加这个属性需要我们在根布局中添加（AS会有提示的）
```
xmlns:app="http://schemas.android.com/apk/res-auto"  

```
![效果图](http://img.blog.csdn.net/20160913005028440?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)


#### Toolbar  自定义标题 大小颜色


定义 Style 样式
```
<style name="Theme.ToolBar.Base.Title" parent="@style/TextAppearance.Widget.AppCompat.Toolbar.Title">
    <item name="android:textSize">16sp</item>
    <item name="android:textColor">@android:color/white</item>
</style>
<style name="Theme.ToolBar.Base.Subtitle" parent="@style/TextAppearance.Widget.AppCompat.Toolbar.Subtitle">
    <item name="android:textSize">11sp</item>
    <item name="android:textColor">@color/toolbar_subTile_color</item>
</style>

```

引用样式：

1. 在java代码中引用：
```
mToolbar.setTitleTextAppearance(this,R.style.Theme_ToolBar_Base_Title);
mToolbar.setSubtitleTextAppearance(this,R.style.Theme_ToolBar_Base_Subtitle);
```
2. xml 中引用

```
app:titleTextAppearance="@style/Theme.ToolBar.Base.Title"
app:subtitleTextAppearance="@style/Theme.ToolBar.Base.Subtitle"

```

##  Toolbar  设置menu 菜单


![1](https://github.com/HanteIsHante/file/blob/master/toolbar%201.png)  

![2](https://github.com/HanteIsHante/file/blob/master/toolbar%202.png)



> menu

```
<!-
1、always：使菜单项一直显示在ToolBar上。
2、ifRoom：如果有足够的空间，这个值会使菜单项显示在ToolBar上。
3、never：使菜单项永远都不出现在ToolBar上,在…的子项中显示。
4、withText：使菜单项和它的图标，菜单文本一起显示。-->

<item
    android:id="@+id/action_edit"
    android:icon="@mipmap/ic_launcher"
    android:orderInCategory="80"
    android:title="edit"
    app:showAsAction="ifRoom" />

<!--点击这个图标展开搜索-->
<item
    android:id="@+id/action_search"
    android:title="dd"
    android:orderInCategory="90"
    app:showAsAction="collapseActionView|ifRoom"
    app:actionViewClass="android.support.v7.widget.SearchView"
    android:icon="@mipmap/ic_launcher"
    />

<!--这两item是隐藏在右上角三个圆点里面的-->
<item
    android:id="@+id/item1"
    android:title="overflow"
    app:showAsAction="never" />

<item
    android:id="@+id/item2"
    android:title="overflow"
    app:showAsAction="never" />

</menu>


```
 

> activity  种

```
  /**菜单控件的一些点击事件*/
    toolbar.setOnMenuItemClickListener(new Toolbar.OnMenuItemClickListener() {
        @Override
        public boolean onMenuItemClick(MenuItem item) {
            switch (item.getItemId()) {
                case R.id.action_edit:
                    Toast.makeText(Main2Activity.this, "action_edit",Toast.LENGTH_SHORT).show();
                    break;
                case R.id.action_search:
                    Toast.makeText(Main2Activity.this, "action_search",Toast.LENGTH_SHORT).show();
                    break;
                case R.id.item1:
                    Toast.makeText(Main2Activity.this, "item1",Toast.LENGTH_SHORT).show();
                    break;
                case R.id.item2:
                    Toast.makeText(Main2Activity.this, "item2",Toast.LENGTH_SHORT).show();
                    break;
            }
            return true;
        }
    });
    
    //如果有Menu,创建完后,系统会自动添加到ToolBar上
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    super.onCreateOptionsMenu(menu);
    getMenuInflater().inflate(R.menu.menu_main, menu);

    /**搜索按钮的相关逻辑*/
    MenuItem menuItem=menu.findItem(R.id.action_search);//
    searchView= (SearchView) MenuItemCompat.getActionView(menuItem);//加载searchview
    searchView.setOnQueryTextListener(new SearchView.OnQueryTextListener() {
        @Override
        public boolean onQueryTextSubmit(String query) {
            Toast.makeText(Main2Activity.this, query,Toast.LENGTH_SHORT).show();
            return true;
        }

        @Override
        public boolean onQueryTextChange(String newText) {
            if (TextUtils.isEmpty((newText))){
                Toast.makeText(Main2Activity.this,"isEmpty",Toast.LENGTH_SHORT).show();
            }else{
                Toast.makeText(Main2Activity.this, newText,Toast.LENGTH_SHORT).show();
            }

            return true;}
    });//为搜索框设置监听事件
    searchView.setSubmitButtonEnabled(true);//设置是否显示搜索按钮
    searchView.setQueryHint("查找");//设置提示信息
    searchView.setIconifiedByDefault(true);//设置搜索默认为图标
    return true;
}
    
     

```
> 另一中添加menu 方式：

```
  //添加溢出菜单
       toolbar.inflateMenu(R.menu.setting_menu);
       // 添加菜单点击事件
       toolbar.setOnMenuItemClickListener(new Toolbar.OnMenuItemClickListener() {
           @Override
           public boolean onMenuItemClick(MenuItem item) {
               switch (item.getItemId()){
                   case R.id.item_setting:
                       //点击设置菜单
                       break;
               }
               return false;
           }
       }); 
```







####  [解决 软键盘弹出 toolbar  遮挡问题](https://juejin.im/entry/58f8a8efda2f60005da90844)

```
private View ll_root;
/**
 * 窗体控件上一次的高度,用于监听键盘弹起
 */
private int mLastHeight;


//onCreate中执行
final View decorView = this.getWindow().getDecorView();//获取window的视图
decorView.getViewTreeObserver().addOnGlobalLayoutListener(
        new ViewTreeObserver.OnGlobalLayoutListener() {
            @Override
            public void onGlobalLayout() {
                Rect r = new Rect();
                decorView.getWindowVisibleDisplayFrame(r);
                //window视图添加控件此方法可能会被多次调用,防止重复调用
                if (mLastHeight != r.bottom) {
                    mLastHeight = r.bottom;
                    ViewGroup.LayoutParams params = ll_root.getLayoutParams();
                    params.height = r.bottom - ll_root.getTop();
                    ll_root.setLayoutParams(params);
                }
            }
        });

```





