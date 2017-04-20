
# ConstraintLayout 


 #### 隐藏视图后，布局遭到破坏：
  
```
app:layout_goneMargin
```

### [Guideline](https://developer.android.com/reference/android/support/constraint/Guideline.html) 使用的属性


> Guideline 是用来辅助定位的一个不可见的元素
 
 Guideline 是 ConstraintLayout 中一个特殊的辅助布局的类。相当于一个不可见的 View，使用 ConstraintLayout 可以创建水平或者垂直的参考线，其他的 View 可以相对于这个参考线来布局。

 
 
```

android_orientation 控制 Guideline 是横向的还是纵向的
layout_constraintGuide_begin 控制 Guideline 距离父容器开始的距离
layout_constraintGuide_end 控制 Guideline 距离父容器末尾的距离
layout_constraintGuide_percent 控制 Guideline 在父容器中的位置为百分比,可以指定位于布局中所在的百分比，比如距离左边 2% 的位置
 

 
```

1 垂直 Guideline 的宽度为 0， 高度为 父容器（ConstraintLayout）的高度
2 水平 Guideline 的高度为 0， 宽度为 父容器（ConstraintLayout）的宽度
3 参考线的位置是可以移动的。

例：

 ```
<android.support.constraint.ConstraintLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
 
    <android.support.constraint.Guideline
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/guideline"
            app:layout_constraintGuide_begin="100dp"
            android:orientation="vertical"/>
 
    <Button
            android:text="Button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/button"
            app:layout_constraintLeft_toLeftOf="@+id/guideline"
            android:layout_marginTop="16dp"
            app:layout_constraintTop_toTopOf="parent" />
 
</android.support.constraint.ConstraintLayout>

 


```






