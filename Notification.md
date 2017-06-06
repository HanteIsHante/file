# Notification



> 关于Notification的Flags

- notification.flags = Notification.FLAG_NO_CLEAR; // 点击清除按钮时就会清除消息通知,但是点击通知栏的通知时不会消失  

- notification.flags = Notification.FLAG_ONGOING_EVENT; // 点击清除按钮不会清除消息通知,可以用来表示在正在运行  

- notification.flags = Notification.FLAG_AUTO_CANCEL; // 点击清除按钮或点击通知后会自动消失  

- notification.flags = Notification.FLAG_INSISTENT; // 一直进行，比如音乐一直播放，知道用户响应  


