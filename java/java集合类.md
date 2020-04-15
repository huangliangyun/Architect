#### 问题

+ 集合在迭代的过程中，插入或删除数据会怎样？
+ 迭代器原理？
+ ArrayList和LinkedList的区别？
+ HashMap和ConcurrentHashMap，HashMap的初始化容量，扩容机制，HashMap怎么获取所有的Key？
+ hashMap 可以并发读么？并发写会有什么问题？
+ HashMap和HashTable的区别。HashTable的初始容量扩容，扩容多少倍？
+ concurrentHashMap的size()？
+ hashSet的底层原理，提问如果添加对象要注意什么？
+ 阻塞队列和一般队列有什么区别，你能说出几种，作用，场景？

#### 答案

+ 集合在迭代的过程中，插入或删除数据会怎样？
集合在使用迭代的时候，不能使用集合本身的add，remove会抛出异常，使用迭代器remove是可以的。
https://blog.csdn.net/qq_36850813/article/details/80313730


+ 迭代器原理？
+ ArrayList和LinkedList的区别？
+ HashMap和ConcurrentHashMap，HashMap的初始化容量，扩容机制，HashMap怎么获取所有的Key？


+ hashMap 可以并发读么？并发写会有什么问题？
1、如果只是写，没有问题，但1.7多线程的情况，put后可能导致get死循环
2、并发写可能导致元素覆盖丢失的情况
https://blog.csdn.net/Javazhoumou/article/details/100586571


+ HashMap和HashTable的区别。HashTable的初始容量扩容，扩容多少倍？
1）HashMap线程不安全，但是效率高，HashTable线程安全，但是效率低
2）HashMap允许Key为null，存放在数组第0个位置，HashTable不允许Key为空，存放空Key直接报错
3）HashTable1.2开始就已经废弃使用，加载因子0.75，默认容量11，扩容2*数组长度+1


+ concurrentHashMap的size()？
https://www.cnblogs.com/maratong/p/12345595.html


+ hashSet的底层原理，提问如果添加对象要注意什么？
HashSet是将内容存在了HashMap的key里面，value只是一个占位符。
需要重写hashCode和equal，否则对象会出现重复。
https://blog.csdn.net/qq_32059827/article/details/51580642


+ 阻塞队列和一般队列有什么区别，你能说出几种，作用，场景？
阻塞队列如果为空，从队列中获取元素将被阻塞，直到线程插入元素，阻塞队列满时，添加会阻塞。
LinkedBlockingQueue
