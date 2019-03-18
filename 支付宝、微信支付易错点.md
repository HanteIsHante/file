
# Alipay
> 注意事项：
1. 调用Aliapay SDK 的请求拼装字符串一定要和签名的顺序一致，否则调不起来支付详情页面
2. 如果调 sdk 时报系统繁忙，稍后再试， 原因可能由于其中某个字段不符合标准， 比如要求某个字段16位，但给的只有12位，少几位的情况；



# WechatPay

> 注意事项：

1. 微信文档有错误， 一定要注意， 比如prepayID 标有32位，其实是错误的，得到签名后的 prepayID  是多少位就传进微信SDK 多少位
2. 需要在 release 版下验证是否能够调起支付详情页面，在debug 版下，会产生errorCode -1;
2. 微信平台上的应用签名可以改成debug 版签名用来测试，发布 release 版时更改成release 版即可；
3. 微信支付(分享) 结果回调需在${applicationId}.wxapi.WXEntryActivity 下才能接收到, [通过"activity-alias" 标签来引向该回调目录](http://www.jianshu.com/p/d6395d947e3d), 同时要注意： 要指向的那个activity 须 在 activity-alias 前注册定义否则重定向可能会失败.


