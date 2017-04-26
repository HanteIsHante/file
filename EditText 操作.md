
# EditText

> EditText 右侧图标点击清除写入内容, 利用 EditText 自带属性，但可操控性差

```
 <EditText
        android:id="@+id/edit_text"
        android:layout_width="368dp"
        android:layout_height="wrap_content"
        android:drawableRight="@mipmap/ic_launcher"
        tools:ignore="LabelFor,MissingConstraints,TextFields"/>

```

```
edit_text.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch (View v, MotionEvent event) {
                // et.getCompoundDrawables()得到一个长度为4的数组，分别表示左右上下四张图片
                Drawable drawable = edit_text.getCompoundDrawables()[2];
                //如果右边没有图片，不再处理
                if(drawable == null) {
                    return false;
                }
                // 如果不是按下事件，不在处理
                if(event.getAction() != MotionEvent.ACTION_UP) {
                    return false;
                }
                if(event.getX() > edit_text.getWidth() - edit_text.getPaddingRight()
                        - drawable.getIntrinsicWidth()) {
                    edit_text.setText("");
                }
                return false;
            }
        });

```

[自定义输入框](https://github.com/EoniJJ/PasswordView/)


[ android 中如何限制 EditText 最大输入字符数](http://blog.csdn.net/fulinwsuafcie/article/details/7437768)





 
[自定义输入密码框](https://github.com/tianshaojie/Android-PasswordInputView)

[一个不错的自定义输入密码框](https://github.com/EthanCo/PasswordInput)




# EditText  属性

[Android EditText属性解析](http://www.jianshu.com/p/c14f4d97b845#)

### EditText 去掉下划线、光标不可见

```
 android:background="@null"
 android:cursorVisible="false"
```
#### 设置光标颜色
 
在使用EditText的XML 文件中加入一个属性：
```
android:textCursorDrawable="@null" 
```
#android:textCursorDrawable#   这个属性是用来控制光标颜色的，
"@null"   是作用是让光标颜色和text color一样
比如 android:textCursorDrawable="@color/black_color"就可以设置成黑色。pad上面很多光标颜色和背景色一样。	
 

####  [动态设置光标颜色](http://blog.csdn.net/qq_30247473/article/details/50422245)

  反射办法修改输入框光标颜色完成
  ```
try {
            Field f = TextView.class.getDeclaredField("mCursorDrawableRes");
            f.setAccessible(true);
            f.set(editPhoneNum, R.drawable.cursor);
        } catch (Exception ignore) {}

 ``` 

```
<shape xmlns:android="http://schemas.android.com/apk/res/android"  
    android:shape="rectangle" >  
  
    <solid android:color="#ff000000" />  
  
    <size android:width="1dp" />  
  
</shape>  
```




### edittext有没有获取焦点

```

EditText.setOnFocusChangeListener(new View.OnFocusChangeListener() {  
       
    @Override  
    public void onFocusChange(View v, boolean hasFocus) {  
        if(hasFocus){//获得焦点  
               
        }else{//失去焦点  
             
        }  
    }             
});
```


### 监控软键盘是否弹出

> InputMethodManager有一个方法isActive（View view）：如果view是输入法的活动view，则返回true。也就是说，如果是由view触发弹出软键盘，则返回true

```
if(isActive（edittext）)  
    隐藏键盘  

```

接着让另一个view强制获取焦点,这样isActivite(ediitext)就为false.

```
InputMethodManager inputMethodManager = (InputMethodManager)getActivity().getSystemService(Context.INPUT_METHOD_SERVICE);<br>private boolean hideKeyboard(){  
        if(inputMethodManager.isActive(searchEditText)){
        //因为是在fragment下，所以用了getView()获取view，也可以用findViewById（）来获取父控件  
            getView().requestFocus();//使其它view获取焦点.这里因为是在fragment下,所以便用了getView(),可以指定任意其它view  
            inputMethodManager.hideSoftInputFromWindow(getActivity().getCurrentFocus().getWindowToken(),                      InputMethodManager.HIDE_NOT_ALWAYS);  
            return true;  
        }  
        return false;  
    }   


```


###  Editext 改变hint 提示文字

1. xml 布局中 修改 hint  属性
2. EditPhoneNum.setHint(getResources().getString(R.string.input_new_phone));








