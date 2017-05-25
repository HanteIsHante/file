



#  BaseActivity 实现DrawerLayout Navigation Drawer

### 设置 Navigation Drawer在BaseActivity 布局

 ```
 
 <?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout
    android:id="@+id/drawer_layout"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <!-- 主内容布局 -->
    <FrameLayout
        android:id="@+id/content_frame"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
    <!-- 侧滑菜单 -->
    <ListView
        android:id="@+id/left_drawer"
        android:layout_width="240dp"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:background="#111"
        android:choiceMode="singleChoice"
        android:divider="@android:color/transparent"
        android:dividerHeight="0dp"/>
</android.support.v4.widget.DrawerLayout>
 
 ```


### BaseActivity

```

public class BaseActivity extends AppCompatActivity {
    
    protected DrawerLayout drawerLayout;
  
    protected FrameLayout frameLayout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }

    /**
    * 重写setContentView，以便于在保留侧滑菜单的同时，让子Activity根据需要加载不同的界面布局
    */
    @Override
    public void setContentView(@LayoutRes int layoutResID) {
        drawerLayout = (DrawerLayout) getLayoutInflater().inflate(R.layout.activity_base, null);
        frameLayout = (FrameLayout) drawerLayout.findViewById(R.id.content_frame);
        // 将传入的layout加载到activity_base的content_frame里面
        getLayoutInflater().inflate(layoutResID, frameLayout, true);
        super.setContentView(drawerLayout);
 
    }
 
}

```

### 创建MainActivity继承BaseActivity ：

```
public class MainActivity extends BaseActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}

```

# 实现DrawerLayout 不覆盖主布局


设置监听

```
 DrawerLayout.DrawerListener listen = new DrawerLayout.DrawerListener() {

        @Override
        public void onDrawerSlide(View drawerView, float slideOffset) {
              //slideOffset.0-1.0，是一个相对整个抽屉宽度的比例
              //所以要准换成
              float  scrollWidth = slideOffset * 侧拉栏ID.getMeasuredWidth();
              //setScroll中的参数，正数表示向左移动，负数向右
              主布局id.setScrollX((int)(1*scrollWidth));
        }

        @Override
        public void onDrawerOpened(View drawerView) {
           
        }

        @Override
        public void onDrawerClosed(View drawerView) {
           
        }

        @Override
        public void onDrawerStateChanged(int newState) {

        }
    };

```

 ### drawerlayout 拉出后会有一个变暗的效果，如果想取消这种效果，可以添加:

```
drawer_layout.setScrimColor(0x00ffffff);
```

这一句，将整个屏幕保持高亮。



###  通过 button 打开关闭 DrawerLayout
 
 打开
```
 drawer_layout_root.openDrawer(菜单ID);

```
关闭
```
drawer_layout_root.closeDrawer(菜单ID);
```


### 返回键

```
  @Override
    public void onBackPressed () {
        if(drawerlayout.isDrawerOpen(GravityCompat.START)) {
            drawerlayout.closeDrawer(GravityCompat.START);
        } else {
            super.onBackPressed();
        }
    }

```
