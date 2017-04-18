
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
 
[自定义输入密码框](https://github.com/tianshaojie/Android-PasswordInputView)

[一个不错的自定义输入密码框](https://github.com/EthanCo/PasswordInput)




# EditText  属性

[Android EditText属性解析](http://www.jianshu.com/p/c14f4d97b845#)

### EditText 去掉下划线、光标不可见

```
 android:background="@null"
 android:cursorVisible="false"
```



