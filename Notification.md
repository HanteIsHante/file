# Notification



> 关于Notification的Flags

- notification.flags = Notification.FLAG_NO_CLEAR; // 点击清除按钮时就会清除消息通知,但是点击通知栏的通知时不会消失  

- notification.flags = Notification.FLAG_ONGOING_EVENT; // 点击清除按钮不会清除消息通知,可以用来表示在正在运行  

- notification.flags = Notification.FLAG_AUTO_CANCEL; // 点击清除按钮或点击通知后会自动消失  

- notification.flags = Notification.FLAG_INSISTENT; // 一直进行，比如音乐一直播放，知道用户响应  



> Notification  点击跳转， 需要给它一个PendingIntent，让这个通知能跳转到应用。如果应用已退出，则启动；如果应用是通过Home键回到桌面的，则进入到应用之前的界面不重新启动。这个PendingIntent需要传一个intent，就是通过这个Intent来实现的， 如果已在应用当前界面则不需要重新创建


```

        Intent intent = new Intent(Intent.ACTION_MAIN);
        intent.addCategory(Intent.CATEGORY_LAUNCHER);
        intent.setComponent(new ComponentName(context, HomeActivity.class));
        intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_RESET_TASK_IF_NEEDED);
        PendingIntent contentIntent = PendingIntent.getActivity(context, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);

```
