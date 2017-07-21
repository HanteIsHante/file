# ADB

> 测量冷启动时间
```
    adb shell am start -W [packageName]/[packageName.MainActivity]
```

> 导出数据库文件

```
adb exec-out run-as cc.netpas.android_firewall cat /data/user/0/cc.netpas.android_firew
all/databases/数据库文件 > 导出文件名

```
