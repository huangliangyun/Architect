#### 问题
+ 1、继承与接口
+ 2、贪心算法、冒泡排序、二分法
+ 3、红黑树、二叉树、哈曼夫树
+ 4、hashmap的底层实现原理
+ 5、tcp/ip
+ 6、Tomcat与nginx各自的优点
+ 7、java中的四大引用、说说虚引用
+ 8、谈谈spring AOP
+ 9、vue
+ 10、对springcloud的认识
+ 11、对Hadoop生态与人工智能的了解
+ 12、Redis缓存机制
+ 13、wait方法与sleep方法的区别
+ 14、垃圾回收机制
+ 15、静态变量
+ 16、git
+ 17、soa架构


#### 答案 

+ 1、继承与接口  
1）抽象类需要被子类继承，接口需要被实现。  
2）抽象类有构造方法，但不能被实现。接口没有构造方法，没有非静态方法的实现，可以定义default方法实现。  
3）抽象类主要用来抽象类别，接口主要用来抽象功能。  
4）抽象类中的变量可以是普通变量，接口中的只能是公共的静态常量。  


+ 2、贪心算法、冒泡排序、二分法
贪心算法：考虑的不是整体，而是局部的最优解


+ 3、红黑树、二叉树、哈曼夫树
红黑树：特殊的二叉树
1、每个节点只能是红色或者是黑色
2、根节点必须是黑色
3、红色节点，叶子节点只能是黑色
4、从任一节点到每个叶子节点所有路径都包含相同数目的黑色节点

满二叉树：二叉树的层数为k，节点数为2^k-1
完全二叉树：深度为k，除k层外，其余各层节点都达到最大个数，第k层节点都连续集中在最左边
平衡二叉树：左子树和右子树深度只差绝对值不超过1
最优二叉树（哈夫曼数）：带权路径长度最短的数，权值较大的节点离根较近

+ 4、hashmap的底层实现原理
1.7：数组+链表 ，Entry，多线程扩容死循环问题
1.8 数组+链表+红黑树，Node，解决死循环

+ 5、tcp/ip
TCP 传输层
IP 网络层
传输控制协议/网际协议
TCP 传输控制协议，位于 IP 协议之上，基于 IP 协议提供可靠的，字节流形式的通信，是 HTTP 协议得以实现的基础。
HTTP是一个协议，不关心寻址，路由，数据完整性等传输细节，这些都是由下层来处理，TCP/IP协议刚好满足这些要求，所以HTTP协议就运行在了TCP/IP之上

+ 6、Tomcat与nginx各自的优点
Tomcat 是 Java服务器，Servlet解析器
Nginx 可以做，虚拟主机，反向代理，负载均衡，故障转移
Nginx 处理静态服务器，Toncat处理动态服务器


+ 7、java中的四大引用、说说虚引用
强引用：new 一个对象，垃圾收集器不会收集
软引用：内存不足就会回收，SoftReference，实现敏感缓存
弱引用：不能避免垃圾回收，WearkReference，缓存
虚引用：也叫幻象引用，=null,不能通过他访问对象
强可达，软可达，弱可达，幻象可达，不可达


+ 8、谈谈spring AOP

+ 9、vue
+ 10、对 springcloud 的认识
1、微服务解决方案
2、SpringCloud 基于 SpringBoot ，关注全局微服务治理。
3、提供组件 eureka，zuul，hystrix，feign，ribbon，config，zipkin
4、二代 Spring Cloud Alibaba



+ 11、对Hadoop生态与人工智能的了解
机器学习：一种实现人工智能的方法
深度学习：一种实现机器学习的技术


+ 12、Redis缓存机制


+ 13、wait方法与sleep方法的区别
1、wait 属于 Object，sleep 属于 Thread
2、wait 让出 CPU 和锁资源，sleep 让出 CPU，不让出锁资源
3、wait 通过 notify或者notifyAll唤醒，sleep时间到自动唤醒
4、wait 必须和 sync 一起使用
https://blog.csdn.net/qq_39907763/article/details/79301813?depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1&utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1

+ 14、垃圾回收机制


+ 15、静态变量
静态变量的引用在方法区，值在堆区
在 jdk8 的 hotspot 虚拟机中，静态变量在逻辑上属于方法区，而实际上是存储在堆中的 class 对象中。

+ 16、git


+ 17、soa架构
SOA 是微服务的前身，微服务由 SOA 演进而来，SOA 架构就是将业务逻辑层提取出来，将相似的业务逻辑形成一个服务，提供外部访问接口，服务之间访问通过 RPC（Remote Procedure Call) 调用实现。
