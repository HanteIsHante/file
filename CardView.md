
# CardView



[Android 使用 CardView 轻松实现卡片式设计](https://juejin.im/entry/5806cbfca0bb9f00589d86a9)



## CardView  点击抬升效果

> res/animator/touch_raise.xml

```
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:state_enabled="true"
        android:state_pressed="true">
        <objectAnimator
            android:duration="@android:integer/config_shortAnimTime"
            android:propertyName="translationZ"
            android:valueTo="8dp"
            android:valueType="floatType" />
    </item>
    <item>
        <objectAnimator
            android:duration="@android:integer/config_shortAnimTime"
            android:propertyName="translationZ"
            android:valueTo="0dp"
            android:valueType="floatType" />
    </item>
</selector>

```

CardView布局中加入属性android:stateListAnimator="@animator/touch_raise"
