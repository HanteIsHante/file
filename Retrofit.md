
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



##  @Field，@FieldMap
  
  > 用于@post请求方式时传递简单的键值对，额外需要添加@FormUrlEncoded表示表单提交。

1. 如果在@post请求中使用@Field和@FieldMap时去掉@FromUrlEncoded，那么程序会抛出java.lang.IllegalArgumentException: @Field parameters can only    be used with form encoding. (parameter #1)的错误异常。

2. 如果将@FromUrlEncoded添加在@GET上面，同样的也会抛出
   java.lang.IllegalArgumentException:FormUrlEncoded can only be specified on HTTP methods with request body (e.g., @POST).的错误异常。
  
3. 如果请求为@POST，最好传递参数时使用@Field、@FieldMap并且需要加上@FormUrlEncoded。因为@Query和@QueryMap都是将参数拼接在url后面的，而@Field或    @FieldMap传递的参数时放在请求体的。  
  
## @URL

 使用全路径复写baseUrl，适用于非统一baseUrl的场景，意思是当@GET或@POST注解的url为全路径时（如果和baseUrl不是一个路径），会直接使用@Url注解中新的路  径。
  
## @Path
  
  用于替换和动态更新,如下所示使用@Path时，id 所表示的路径中不能包含”/”，否则会将其转化为%2F。
  
  ```
  @GET("group/{id}/users")
  Call<TextBean> getUsers(@Path("id") int id);
  ```
  
  ## @Streaming
   
   用于下载大文件
  
  ```
  @Streaming/*下载大文件需要注入，防止下载过程中写入到内存中*/
  @GET
  Call<ResponseBody> downloadFile(@Url String fileUrl);
  ```
  ## @Part
  
  实现图片和参数上传，如果图片不确定  @PartMap() Map<String, RequestBody> maps  代替  @Part MultipartBody.Part file

  ```
  @FormUrlEncoded
  @Multipart
 @POST("API/public")
 Call<ResponseBody> upload(@FieldMap Map<String, String> params,//参数集合
                        @Part("description") RequestBody description,//图片描述
                        @Part MultipartBody.Part file);//图片
  
  ```
  
  ```
  
 // 封装 请求参数集合 map
 ...
// 封装 请求RequestBody
RequestBody requestFile =
      RequestBody.create(MediaType.parse("multipart/form-data"), file);
MultipartBody.Part body =
      MultipartBody.Part.createFormData("image", file.getName(), requestFile);
String descriptionString = "添加文件描述";
RequestBody description =
      RequestBody.create(MediaType.parse("multipart/form-data"), descriptionString);
//
Call<ResponseBody> call = service.upload(maps,description,body);

```
## @Body

> 也可以实现图片和参数的上传

```
 //上传图片
  @POST("API/public/ChangeUserImg")
  Flowable<ResponseBody> upFile(@Body RequestBody Body);
  ```
  ```
RequestBody body = new MultipartBody.Builder()
            .setType(MultipartBody.FORM)
            .addFormDataPart("uid", mUid)
            .addFormDataPart("newUserImg",file.getName(),RequestBody.create(MediaType.parse("image/*"), file))
            .build();
Call<ResponseBody> call = service.upFile(body);
...

```
> 上传json数据

```
@POST("/uploadJson")
Call<ResponseBody> postJson(@Body RequestBody jsonBody);

```

```
RequestBody body= 
             RequestBody.create(okhttp3.MediaType.parse("application/json; charset=utf-8"), jsonString);
Call<ResponseBody> call = APIService.postJson(requestBody);
...
```
 
