#### 问题
+ int float short double long char 占字节数？
+ int 范围？float 范围？
+ 内部类可以引用包含他的类的成员吗，如果可以，有没有什么限制吗？
+ 基本数据类型和成员变量类型，基本数据类型创建的内存在哪？
+ 子类重写父类方法，声明子类，还会调用父类方法吗？
+ 符号“==”比较的是什么？
+ 为什么重写 equal 之后要重写 hashCode？
+ 多态的理解？
+ lambda 表达式中使用外部变量，为什么要 final？
+ 为什么String是不可变的？"+" 的问题？
+ String hashCode源码?
+ String，StringBuffer 和 StringBulider 区别？
+ 抽象类和接口的区别？
+ error 和 exception 有什么区别?
+ final 修饰的类，方法，变量的区别？
+ 组合？继承？依赖？区别？
+ 4种权限修饰符的区别？
+ IF 和 Switch 的区别？
+ 深拷贝和浅拷贝，区别？怎么实现？
+ for，forEach，迭代器的区别?
+ 4 种引用如何实现?
+ Object类有多少个方法?
+ Java元注解?
+ 为什么 wait，notify，notifyAll 被定义在 Object 里面?
+ 为什么 wait，notify，notifyAll 必须在同步快或者同步方法之中使用？
+ 阻塞队列的实现方式？

#### 答案

+ int float short double long char 占字节数？  
int：4byte  
float：4byte  
short：2byte  
long：8byte  
double：8byte  
char：2byte  
byte：1byte（-128~127）  
boolean：1byte  
https://blog.csdn.net/i6223671/article/details/88368926  


+ int 范围？float 范围？  
int：-2^31~2^31-1  
float：[-3.4e+38,-1.4e-45]∪[1.4e-45,3.4e+38]  
https://blog.csdn.net/weixin_39460458/article/details/79995203  


+ 内部类可以引用包含他的类的成员吗，如果可以，有没有什么限制吗？  
如果不是静态内部类，完全可以。没有什么限制！ 在静态内部类下，不可以访问外部类的普通成员变量，而只能访问外部类中的静态成员。  


+ 静态成员变量放在哪？基本数据类型创建的内存在哪？  
静态变量：引用存放在方法区，值放在堆的Class，一个静态变量只会有一个内存空间。一个类的静态方法只能访问静态属性，一个类的静态方法不能直接调用非静态方法。  
基本数据类型存放在哪？  
方法外定义句局部变量，放在堆中  
如果在方法中，则在局部变量表中  
https://www.cnblogs.com/hithlb/p/4872373.html  


+ 子类重写父类方法，声明子类，还会调用父类方法吗？  
不会  
调用顺序：  
父类静态代码块>子类静态代码块>父类成员>父类非静态代码块>父类构造方法>子类成员>子类非静态代码块>子类构  造方法  
https://blog.csdn.net/nsjlive/article/details/89501836  


+ 符号“==”比较的是什么？  
==可以比较基本数据类型和引用类型，基本数据类型比较的是数值，在比较引用类型时，除了比较数值外，还要比较引用地址，两者都相等时，结果才是true。  


+ 为什么重写 equal 之后要重写 hashCode  
因为我们要遵循hashCode相等，对象的值不一定相等，如果equal比较的对象内容相等，hashCode一定相等。所以重写equal方法的时候，需要重写hashCode，保证原则不变。  


+ 多态的理解  
多态是同一个行为的不同表现方式，Java多态主要体现在两个方面，重载和重写。重载时，调用相同的方法，但是参数不同，可以做出不同的行为。重写时，父类的方法如果无法满足子类，子类可以重写父类的方法，需要遵循两同，两小，一大原则。  


+ lambda 表达式中使用外部变量，为什么要 final？  
保护数据的一致性  
https://blog.csdn.net/qq_39111325/article/details/86441994  


+ 为什么String是不可变的？"+" 的问题？  
String是一个final类，意味着他是不能被继承的，String的底层数组char是一个私有final成员，这样做首先是安全，比如hashMap中用string做为键，不会出现string变化，导致违反唯一键。另外节约内存。  
但数组是一个引用类型，所以只能限制引用不能被改变，也就是说值是可以改变的。但String使用外部的char构造对象，是重新复制了一遍外部的char数组，从而不会让外部的char数组影响到String。  
substring如果不是切割完整的对象，就会创造一个完整的对象。  
如果+的不是变量，编译时计算，是变量，运行时计算。  
https://blog.csdn.net/qq_41097354/article/details/90140394  


+ String hashCode源码?  
默认情况下Object中的hashCode返回32位的JVM内存地址。  
https://blog.csdn.net/diweikang/article/details/88738358  


+ String，StringBuffer 和 StringBulider 区别？  
String是final修饰的类，所有的属性不可变，保证了线程安全，正因为不可变，所以所有的拼接，剪裁，都会产生新的String对象。  
StringBuffer在各种修改数据的方法上都添加了synchronized关键字，保证了线程安全，但带来了而外的开销。  
StringBuilder去掉了线程安全的部分，减少了开销  。


+ 抽象类和接口的区别？  
1）抽象类需要被子类继承，接口需要被实现。  
2）抽象类有构造方法，但不能被实现。接口没有构造方法，没有非静态方法的实现，可以定义default方法实现。  
3）抽象类主要用来抽象类别，接口主要用来抽象功能。  
4）抽象类中的变量可以是普通变量，接口中的只能是公共的静态常量。  


+ error 和 exception 有什么区别?  
error 会导致程序宕机，不便于也不需要捕获，如OutOfMemoryError，ThreadDeath。  
exception分为可检查异常和不可检查异常，可检查异常必须在代码里面捕获，是编译期检查的异常，如IOException，SQLException。不可检查异常也就是运行时异常（RuntimeException），比如空指针，数组越界。  


+ final修饰的类，方法，变量的区别？  
修饰的类不能内继承，修饰的方法不能被重写，修饰的变量不能被覆盖。  


+ 组合？继承？依赖？区别？  
继承：一个类继承另外一个类的功能，并增加自己的功能  
实现：一个类实现多个接口的功能  
聚合：整体和部分是可以分离的，比如公司和员工  
组合：也称为强聚合，整体和部分是不可分的  
依赖：一个类使用到了另一个类  
关联：关系比依赖强，不存在偶然性，临时性，是长期的  
https://www.cnblogs.com/jiqing9006/p/5915023.html  


+ 4种权限修饰符的区别？  
public 所有地方都能调用  
protected 同一个类，同一个包，子类能调用  
default同一个类，同一个包能调用  
private同一个类才能调用  


+ IF 和 Switch 的区别？  
他们都是条件语句，Switch中的case要求的是常量  


+ 深拷贝和浅拷贝，区别？怎么实现？  
深拷贝是彻底的拷贝，俩对象所有的成员都是独立的一份，而且成员对象也是独立的一份。  
深拷贝如果不够彻底，就是浅拷贝，浅拷贝某些成员变量可能是共享的，值类型在浅拷贝的时候就会复制一个独立的副本，引用数类型在拷贝的时候，只是复制了一个引用。  
Object的clone是一个浅拷贝，如果他拷贝的对象中有其他的对象，那么其中的对象是不会得到彻底的拷贝的。  
Cloneable也能实现深拷贝，但是拷贝不全，我们可以使用commons包下面的SerializaionUtils的clone方法来实现深拷贝。  
https://cloud.tencent.com/developer/article/1362831  


+ for，forEach，迭代器的区别?  
forEach的内部机制就是使用迭代   
https://www.cnblogs.com/DSNFZ/articles/7594756.html  


+ 四种引用如何实现?  
我们先创建一个对象的时候，就是一个强引用，垃圾回收器不会碰这种对象，软引用是当JVM内存不足的时候就会回收这种对象，通常用来实现敏感缓存，使用SoftReference实现。弱引用并不能避免被垃圾回收，也是很多缓存的实现，使用WeakReference实现，当我们把一个对象赋值为null的时候，就是一个幻象引用。  
对应5种可达性级别，分别是强可达，软可达，弱可达，幻象可达，不可达。  
强可达：一个对象可以有一个或多个线程可以不同过各种引用访问到，我们创建一个对象，创建他的线程就是强可达。  
软可达：只能通过软引用访问到的状态。  
弱可达：只能通过若引用访问到的状态，接近finalized状态，弱引用被清除的条件就是finalized。  
幻象可达:被finalized过的对象，只有幻象引用指向这个对象的时候。  


+ Object类有多少个方法?  
clone 创建并返回一个对象的副本  
finalize 垃圾收集器确定不存在对该对象的更多引用是，由对象的垃圾收集器调用次方法  
getClass 返回此Object运行时的类  
hashCode 返回此对象的哈希值  
equal 判断对象是否相等  
toString 返回对象的字符串表示  
wait 让一个线程处于等待状态  
notify 随机唤醒一个线程  
notifyAll 唤醒所有线程  


+ Java元注解?  
@Target 表示注解用在什么地方  
@Retention 表示该注解可以保存的范围  
@Documented 表示该注解标注的元素可以被javadoc此类工具文档化  
@Inherited如果父类中的注解使用@Inherited修饰，子类就能继承父类注解  
https://www.jianshu.com/p/7f54e7250be3  


+ 为什么 wait，notify，notifyAll 被定义在 Object 里面?  
在Java中，任意对象都可以当成锁来使用，所以这些通信方法需要被定义在Obejct里面  


+ 为什么 wait，notify，notifyAll 必须在同步快或者同步方法之中使用？  
确保等待线程从wait()返回时能够感知线程对共享变量作出的修改。如果不在范围内使用，就会抛出异常。  


+ 阻塞队列的实现方式？  
ArrayBlockingQueue，LinkedBlockingQueue，DelayQueue，PriorityBlockQueue  
https://www.cnblogs.com/jackion5/p/11173721.html  



