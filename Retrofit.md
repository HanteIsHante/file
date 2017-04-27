
# Retrofit 2.0









## @GET

> @get请求静态url

```
  //无参数
  @GET("API/public")
  Call<TextBean> getData();

  //只有一个参数且参数key值：uid
  @GET("API/public")
  Call<TextBean> getData(@Query("uid") String uid);

  //参数较多
  @GET("API/public")
  Call<TextBean> getData(@QueryMap Map<String, String> params);

```

> @get请求动态url

```
@GET
  Call<TextBean> getDataUrl(@Url String url);
```

## @POST

> @post请求静态url
```
   //无参数
  @POST("API/public")
  Call<TextBean> postData();

  //一个参数
  @FormUrlEncoded
  @POST("API/public")
  Call<TextBean> postData(@Field("uid") String uid);

  //参数较多
  @FormUrlEncoded
  @POST("API/public")
  Call<TextBean> postData(@FieldMap Map<String, String> params);
```
> @post请求动态url
```
@POST
Call<TextBean> postDataUrl(@Url String url);
```



# 注意事项：

因为Retrofit 2.0使用了新的URL定义方式，BaseUrl与@POST 不是简单的组合在一起，所以BaseUrl根域名和@POST 中路径组合时应按照：BaseUrl: 以 / 结尾，@GET或者@POST: 不以 / 开头的标准，如图所示：

![](http://upload-images.jianshu.io/upload_images/3900300-369bf3bc3d28a586.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### Error

![](http://upload-images.jianshu.io/upload_images/3900300-aabd63beda3632d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3900300-40f629f10cfe61fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)






