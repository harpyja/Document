# Document
学到的技术
1. Java类加载机制： 双亲委派模型 通过代理 将需要加载的类从顶层classloader开始查找并加载 后续的classloader是无法覆盖已经加载的类的
  bootstrap classloader
  external classloader
  application classloader
2. 公平锁 就是 高相应比优先的锁  谁等的时间长 执行时间短 谁优先 不至于产生饥饿现象
3. 可重入锁 sychronize or Lock 不至于循环调用产生死锁 但是sychronize如果是多线程情况下会产生b穷等，Lock可以解决这个问题
4. volital 关键字的目的就是原子更新数据，避免脏读现象发生。 再就是代码不重排序 也是解决多线程的赋值问题。 
5. 抽象类的内部类
由于抽象类是不能被实例化的，所以静态内部类可以通过new 外部类.内部类()来创建内部类的实例。而非静态的内部类则无法被实例化。
6. 内部抽象类
普通内部类需要先实例化外部类，然后在实例化内部类。抽象内部类也是通过此方法实现，只是需要在实例化的时候重写抽象方法。
7.android 11新特性： 每个app的外部存储的权限控制死了，不能访问别的app的文件
8. webview漏洞攻击： 构造intent调取其他app的webview并加载html 由于文件协议 这个html
9. hashmap初始化数组大小是16， 底层数据结构是数组+链表， 为啥hashmap的查找是o1，是因为数组指针 直接用下标访问数组之后访问
10. 有序数组合并的时间复杂度是om+n 空间复杂度是o1
11. hashtable
