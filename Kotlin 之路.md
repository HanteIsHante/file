
# Kotlin






## 优点：
. 不会再有NullPointerException

  . kotlin的null安全主要通过?和!!人为的将变量做了限制
  . 对可空的变量的操作，也要做空判断str?.length
  . 可以直接定义变量var result，kotlin会根据后面的赋值动态的判断result的类型
  . 合理的利用三元操作符?:，对result的数据类型进行控制，并避免空指针异常的问题

 






## 官网还推荐了一个插件：kotlin-android-extensions，能大大减少，甚至消灭findViewById，直接映射xml的组件
[官网说明](https://www.kotlincn.net/docs/tutorials/android-plugin.html)

