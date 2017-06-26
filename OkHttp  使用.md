# OkHttp

![](http://upload-images.jianshu.io/upload_images/1674999-9b8a9e0353734231.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




```
Response response =  OkHttpClient.newCall(request).execute();
if (!response.isSuccessful()) throw new IOException("Unexpected code " + response);
    response.body().charStream() 
```

> ResponseBody类

1 ResponseBody存储了服务端发往客户端的原始字节流。

2 ResponseBody必须被关闭

3 每一个响应体都是一个有限的资源支持。如果没有关闭的响应体将泄漏这些资源，
  并可能最终导致应用程序的速度慢下来或崩溃。通过close()，bytestream()关闭响应体.reader().close(),
  其中bytes()和string()方法会自动关闭响应体。
  
4 响应主体只能被消耗一次。

5 这个类可以用于非常大的响应流。例如，常见的视频流应用的要求。

6 因为这个ResponseBody不缓冲内存中的全部响应，应用程序不能重新读取响应的字节数。
  可以利用 bytes() orstring()，source(), byteStream(), or charStream()等方法，将流内容读入到内存中。

```
response.close();
```

### 取消任务功能

```
 Call call = OkHttpClient.newCall(request)

 call.cancel();
```



### MultipartBody

    看下源码可知它适用于这五种Content-Type:

```

public static final MediaType MIXED = MediaType.parse("multipart/mixed");
public static final MediaType ALTERNATIVE = MediaType.parse("multipart/alternative");
public static final MediaType DIGEST = MediaType.parse("multipart/digest");
public static final MediaType PARALLEL = MediaType.parse("multipart/parallel");
public static final MediaType FORM = MediaType.parse("multipart/form-data");
```

## 注：
1. okhttp 请求头 不支持包含中文， [参考](http://www.jianshu.com/p/ddbe8c637fc5)  及 [博客](http://blog.csdn.net/mobilexu/article/details/50699768)


