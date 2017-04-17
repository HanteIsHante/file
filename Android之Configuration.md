

## Android中Configuration类专门用于描述手机设备上的配置信息,这些配置信息既包括用户特定的配置项,也包括系统的动态设备配置。

Configuration对象的获得:
```
Configuration configuration=getResources().getConfiguration();
```
```

 public int densityDpi;  //得到设备的密度
    public float fontScale; //获取当前用户设置的字体的缩放因子
    public int KeyboardHidden;//该属性会返回一个boolean值用于表示当前的键盘是否可用,该属性不仅会判断系统的硬件键盘,也会判断系统位于屏幕上的软键盘,如果该系统的硬件键盘不可用但软键盘可用该属性会返回KEYBOARDHIDDEN_NO,只有当两个键盘都不可用的时候才返回KEYBOARDHIDDEN_YES
    public int keyboard;//获取当前设备所关联的键盘的类型
    public Locale locale;//获取用于当前的Locale
    public int mcc;//得到移动信号的国家码
    public int mnc;//得到移动信号的网络码
    public int navigation;//判断系统上方向导航设备的类型。该属性的返回值：NAVIGATION_NONAV（无导航）、NAVIGATION_DPAD(DPAD导航）、NAVIGATION_TRACKBALL（轨迹球导航）、NAVIGATION_WHEEL（滚轮导航）
    public int orientation;//得到系统屏幕的方向,该属性将会返回ORIENTATION_LANDSCAPE(横向屏幕),ORIENTATION_PORTRAIT(竖向屏幕),ORIENTATION_SQUARE(方形屏幕)三个属性值之一
    public int touchscreen;//获取系统触摸屏的触摸方式。该属性的返回值：TOUCHSCREEN_NOTOUCH（无触摸屏）、TOUCHSCREEN_STYLUS（触摸笔式触摸屏）、TOUCHSCREEN_FINGER（接收手指的触摸屏）等属性值


```

此外,如果程序需要监听系统设置的更改,这里就需要重写Activity的onConfigurationChanged(Configuration newConfig)的方法,例如我们要实现设置系统的屏幕更改方向并监听,需要有以下几步: 
指定清单文件中的configChanges属性
```
   <activity android:name=".MainActivity"
             android:configChanges="screenSize|orientation">
            <intent-filter>
              <action android:name="android.intent.action.MAIN"/>
              <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
    </activity>

```
设置按钮的点击事件，并重写回调方法:

```
public void changeOri(View view){
        Configuration configuration=getResources().getConfiguration();
        if(configuration.orientation==Configuration.ORIENTATION_LANDSCAPE){
            //当前是横屏，需要更改为竖屏
            MainActivity.this.setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);
        }
        if(configuration.orientation==Configuration.ORIENTATION_PORTRAIT){
            //当前是竖屏，需要更改为横屏
            MainActivity.this.setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
        }
    }

    @Override
    public void onConfigurationChanged(Configuration newConfig) {
        super.onConfigurationChanged(newConfig);
        String screen=newConfig.orientation==Configuration.ORIENTATION_LANDSCAPE?"横屏":"竖屏";
        Toast.makeText(this,"当前屏幕的状态是:"+screen,Toast.LENGTH_SHORT).show();
    }
```
