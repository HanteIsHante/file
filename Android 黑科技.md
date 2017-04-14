

# 应用场景

有一些出厂测试的程序，或者一些隐秘的程序，不能将app的启动图标直接显示到程序列表中，所以我们需要将程序隐藏，通过拨号输入特定的号码或字符来启动程序。

[](http://upload-images.jianshu.io/upload_images/5194858-e81ae4472d1195fd.gif?imageMogr2/auto-orient/strip)


原理

如果你详细研究过android源码（当然本人看的是低版本的你懂的），在联系人模块中有一个文件：
packages/apps/Contacts/src/com/android/contacts/SpecialCharSequenceMgr.java
他里面有一段关键代码是这样写的：
```
/** 
     * Handles secret codes to launch arbitrary activities in the form of *#*#<code>#*#*. 
     * If a secret code is encountered an Intent is started with the android_secret_code://<code> 
     * URI. 
     * 
     * @param context the context to use 
     * @param input the text to check for a secret code in 
     * @return true if a secret code was encountered 
     */  
 static boolean handleSecretCode(Context context, String input) {  
        // Secret codes are in the form *#*#<code>#*#*  
        int len = input.length();  
        if (len > 8 && input.startsWith("*#*#") && input.endsWith("#*#*")) {  
            Intent intent = new Intent(Intents.SECRET_CODE_ACTION,  
                    Uri.parse("android_secret_code://" + input.substring(4, len - 4)));  
            context.sendBroadcast(intent);  
            return true;  
        }  

        return false;  
    }
    
```


可以看到在拨号中当接收到*#*#< code >#*#* 这样的指令时，程序会对外发送广播。这就意味着我们都能够接收这个广播然后做自己想做的事情了









