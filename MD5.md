
# MD5

>android升级的时候，需要下载apk包，为了监测我们下载的apk包是否完整，我们可以使用md5值来监测
本地下载完apk包后，获取文件的md5值，和服务器返回的md5 值最对比判断


##### 获取文件m5d值方法

```

public static String getMd5(File file) throws FileNotFoundException {
        String value = null;
        FileInputStream in = null;
        try {
            in = new FileInputStream(file);
            MappedByteBuffer byteBuffer = in.getChannel().map(FileChannel.MapMode.READ_ONLY, 0, file.length());
            MessageDigest md5 = MessageDigest.getInstance("MD5");
            md5.update(byteBuffer);
            BigInteger bi = new BigInteger(1, md5.digest());
            value = bi.toString(16);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (null != in) {
                try {
                    in.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
        return value;
    }

```
