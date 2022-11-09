# Document
## 学到的技术/复习
1. Java类加载机制： 双亲委派模型 通过代理 将需要加载的类从顶层classloader开始查找并加载 后续的classloader是无法覆盖已经加载的类的
  bootstrap classloader
  external classloader
  application classloader
  双亲委派实际上就是 如果调用子类继承的父类static参数 不会初始化子类
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
11. hashtable是线程安全的 全局锁 sychornize
12. 自旋锁：while穷等，互斥锁：单一线程 读写锁：多读，写只能有一个
13. 公平锁非公平锁：公平锁会在线程刚进来的时候先判断是否有等待
14. 不用重启的xposed： 不把xposed加载到zygote进程中，而是在XposedBridge里判断 fork出来的进程是目标进程再进行加载
15. 工厂模式，观察者模式，代理模式
    工厂模式：适合不经常修改的业务： 接口 继承之后 有需求就得增加。使用抽象工厂模式替代 abstract class 可以不完全实现
16. Xposed为啥能hook？ before和after的本质：把原来的java方法指向了nativemethod 在native中before+调用原javamethod+after实现的前后hook
17. 为啥主线程/ui线程looper不能导致anr？因为looper本身就是没有就阻塞在那，只有ui操作超时了才会发生anr。主线程消息堆积了就会产生异常
    而阻塞在那其实就是pipe机制，没有消息就休眠 有就唤醒执行。
18. applicationThread与ActivityThread的区别？applicationThread是binder 是activityThread 的子类，ActivityThread 就是ui线程，
19. virtualapp多开的解决方式：堆栈是其中一个 再就是能执行shell 那就是万能 再就是通常来看va之后 本身只能获取到自己一个app
20. android5 以后aygote就是两个进程了 一个是32位的 一个是64位的
21. xposed其实就是 dalvik中反射method变量 获取directmethod/nativemethod 找到目标函数 修改为native函数 这个函数就会先调before处理 之后hook 的函数 之后是after
    是在过程中dalvik
22. application启动过程 ui线程先向ams请求bindapplication 在这期间是用的binder binder需要经过 servicemanager获取ams的binder信息和对象 之后再进行访问ams的attachapplication 之后就告诉app说application准备好了，用handler loop到主线程中让主线程准备instrumentation 之后通过类加载传参new Application 之后调oncreate就行了 其实开activity就是把activity类名给ams之后调oncreate
23. 平衡二叉查找树的时间复杂度是ologn， 快排的时间复杂度是不固定的 ologn-on
24. c++ 中 >>相当于除以2取整
25. b 跳转
bl 带返回跳转
blx 带返回状态切换跳转
bx 状态切换跳转
bxxx实现的是短跳转 32m内存的
lr寄存器的值直接给pc 实现长跳转 4g内存中随便跳转

## 深度学习 

1. IOU就是（检测框与真实框的交集除以并集）
2. 这个IOU的评价指标是有个阈值的（threshold）进而引入评价体系TP，FP，TN，FN
    1. TP: True Positive 即IOU > threshold 检测框与真实框的交集大于阈值
    2. FP: False Positive 即IOU < threshold 检测框与真实框交集小于阈值
    3. TN: True Nagative 即IOU = 0 有真实框没有检测框
    4. FN：False Nagative 没有检测框 有真实框 (计算的时候算的是所有的真实框)
3. AP就是平均精度（Average Precision）
    1. Precision = TP/(TP+FP)
    2. Recall = TP(TP+FN)
    3. AP的原始定义是p(r)函数(横坐标为recall，纵坐标为precision)在0到1上的积分
    4. https://blog.csdn.net/beizhengren/article/details/120980881
    5. NMS(非极大值抑制) 就是在选取bounding box的时候选择IOU最大的 其余的一律不算即直接将IOU置0

