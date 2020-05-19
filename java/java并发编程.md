#### 问题

+ 锁和同步的区别？
+ 什么是死锁，如何避免，如何定位？
+ 什么是死锁，写一个死锁代码？
+ AtomicInteger 原子类底层原理？
+ synchronized 如何实现锁的同步？
+ synchronized 锁升级的过程？
+ synchronized锁升级的原理是什么？
+ volatile 的底层实现原理？
+ 什么是原子操作，在 JavaAPI 中有哪些原子类
+ ThreadLocal 作用？
+ ThreadLocal 原理？
+ ThreadLocal 会有什么问题？
+ AQS 是什么？
+ CAS 是什么？
+ synchronized 和 ReentrantLock 区别？
+ synchronized 和 volatile 的区别？
+ volatile 和 AtomicInteger 原子类区别？
+ CountDownLatch 和 CyclicBarrier区别和使用场景？
+ Semaphone 有什么用？
+ happen-before原则有哪些？
+ Copy-On-Write 是什么？


#### 答案

+ 锁和同步的区别？  
线程同步是指在多线程的场景下，由于写操作所造成的数据不一致的安全问题，而使用锁可以解决线程不同步问题。  


+ 什么是死锁，如何避免，如何定位？  
两个或两个以上的进程在执行的过程中，因为争夺资源而造成的一种相互等待的状态，若无外力的作用，他们将无法推进下去。死锁满足四个条件，打破任意一个条件，都能打破死锁。  
1）互斥条件：一个资源每次只能被一个进程使用.  
2）请求和保持：一个进程因请求资源而被阻塞时，对已获的资源保持不放。  
3）不可剥夺:进程以获得资源，在未使用完之前，不可强行剥夺。  
4）循环等待：若干的线程形成一种首尾相接的循环等待资源关系。  


+ 什么是死锁，写一个死锁代码？  

+ 什么是原子操作，在 JavaAPI 中有哪些原子类？  
原子操作是一个不受其他操作影响的操作任务单元。原子操作是在多线程环境下避免数据不一致的必须手段。比如 i++ 就不是一个原子操作，当一个线程读取他的值并 +1 时，另一个线程可能会读到之前的值。  


+ AtomicInteger 原子类底层原理？  
AtomicInteger 是对 int 类型的一个封装，提供原子性的访问和更新操作，原子操作是基于 CAS 操作，他依赖于 Unsafe 提供的一些底层能力，进行底层操作，使用 volatile 修饰 value 字段，保证可见性，Unsafe 会利用 value 字段的内存地址偏移，直接完成操作。  


+ synchronized 如何实现锁的同步？  
1）synchronized 可以锁住一个方法，也可以锁住一个代码块。  
2）如果锁住一个对象，会在这个对象的对象头的标记字段中保存指向 monitor 的地址，这个monitor里面包含了等待获取锁的线程，进入获取锁的线程，以及拥有这个对象锁的线程。  
3）而如果是一个同步方法，则有一个标记位：flags：ACC_SYNCHRONIZED，表示该线程拥有锁。  
4）如果锁的是代码块，每一个对象都和 monitor 关联，某个对象的 monitor 被拥有后就会被锁住，线程执行到 monitorenter，就会尝试获得 monitor，每一个 monitor 维护一个记录被拥有次数的计数器，未被拥有的 monitor 计数器为 0 ，一个线程执行到 monitorenter 后，计数器就会变为1，再次执行到的时候就会+1，不同的线程想获得该 monitor 就会阻塞，同一个线程执行 monitorexit ，就会释放monitor，计数器自减，计数器为0，monitor释放，其他线程获得锁。  


+ synchronized 锁升级的过程？
1）首先是无锁  
2）如果一个线程获取锁，就会使用偏向锁优先于这个线程再次获取锁。  
3）如果获取锁失败，就会升级为CAS轻量级锁，进行短暂的自旋  
4）如果以上都失败，就会升级为重量级锁。重量级锁是通过对象内部的监视器 monitor 实现，其中的 monitor 是通过操作系统底层的 Mutex Lock 实现，操作系统实现线程之间的切换需要从用户态切换到内核态，切换成本非常高。  


+ synchronized锁升级的原理是什么？  
在锁的对象头里面有一个 threadid 的字段，第一次访问的时候，threadid 为空，jvm 让其持有偏向锁，并将 threadid 设置为线程 id，再次进入的时候，就会判断 threadid 和当前线程id是否一致，如果一致就可以直接拿到对象，如果获得不到则升级偏向锁为轻量级锁，通过自旋一定的次数来获得锁，执行一定的次数之后，如果没有获得对象，此时，会把锁由轻量级锁升级为重量级锁。


+ volatile 的底层实现原理？  
volatile 保证线程的可见性以及禁止指令的重排序，但是无法保证原子性。禁止指令重排序在 JVM 底层 volatile 是采用内存屏障来实现的。使用 volatile 关键字时，汇编后就会多出一个 lock 指令，相当于一个内存屏障。  
对该变量进行写操作后，编译器会插入一个写屏障。对该变量读之前，编译器会插入一个读屏障。当一个共享变量被 volatile 修饰时，他会保证修改的值立即刷新到主存，当其他线程需要读取的时候，就会从主内存中读取新值。  

+ ThreadLocal 作用？  
ThreadLocal会对每一个线程创建一个独立的变量副本，线程之间互不影响，提供了get，set，remove，在 get 之前必须 set，否则会抛出异常，场景如数据库链接，session 管理等。  


+ ThreadLocal 原理？  
每一个 Thread 对象都包含一个ThreadLocalMap 类型的成员变量 threadlocals，他存储本线程中所有的 ThreadLocal 对象及其对应的值。进行 set，get 等操作会先获取当前线程对象，然后获取当前的 ThreadLocalMap 对象，再以当前ThreadLocal 对象为key，做相应的处理。 


+ ThreadLocal 会有什么问题？
ThreadLocalMap中，只有 key 是弱引用，value 是强引用，每次 set，get，remove，ThreadLocal都会将 key 为 null 的 Entry 删除，从而避免内存泄露，如果一个线程运行周期较长，把一个大对象放在 LocalThreadMap 中，不再调用 set，get，remove，仍然可能导致内存泄露。这个没有办法通过 ThreadLocal 解决，需要在程序员完成 ThreaLocal 的使用之后手动调用 remove，避免内存泄露。


+ AQS 是什么？  
AQS是同步队列器，是Java提供的底层同步工具，他有一个标记为 state，并使用 CAS 来管理这个同步状态，值为 1 表示线程占用，其他线程进入同步队列等待，同步队列是双向链表。  
如果获得锁的线程需要等待某个条件，就会进入 condition 等待队列，等待队列可以有多个 condition条件满足时，就会从条件队列到等待队列竞争锁。  
例如 ReentrantLock 和 Semaphone 的实现  


+ CAS 是什么？  
CAS 是比较和替换，基于乐观锁。线程在读取数据的时候不加锁，在写数据的时候，先比较值和原来是否相同，如果相同则写回，如果不同则重新执行度流程。  
这个过程可能会产生ABA问题，我们可以添加版本号或者设置时间戳解决。  
CAS机制只能保证一个变量的原子性操作，不能保证整个代码块的原子性。  
CAS 造成 CPU 利用率增加。  


+ synchronized 和 ReentrantLock 区别？  
1）synchronized 是 JVM 层面，ReentrantLock 是 JDK 层面  
2）ReentrantLock 默认为非公平锁，可以实现公平锁，synchronized 只能是非公平锁  
3）ReentrantLock 可以让线程尝试获得锁，在无法获得锁的时候就会进行等待或者立即返回，而synchronized 无法做到。  
4）synchronized 在发生异常的时候，会自动释放线程占有的锁，如果 ReentrantLock 在发生异常的时候，如果没有使用 unlock 释放，就会造成死锁，因此使用 ReentrantLock 的时候需要在 finally 中释放锁。  
5) ReentrantLock 只能用于代码块，synchronized 可以用于方法，代码块。  
6) ReentrantLock 提供了一个 Condition 条件，可以用来分组唤醒线程，而synchronized 要么随机唤醒一个线程，要么全部唤醒。  
7）ReentrantLock 提供了一种能够立即中断等待锁的机制，通过 lock.lockInterrupttible() 实现  
8）都是可重入锁，悲观锁  


+ synchronized 和 volatile 的区别？  
1）volatile 修饰变量，synchronized 修饰方法，代码块  
2）volatile 保证变量的可见性，禁止指令重排序，但不保证变量的原子性，synchronized 保证可见性和原子性  


+ volatile 和 AtomicInteger 原子类区别？  
1）volatile 变量可以确保先行关系，即写操作会发生在后续的读操作之前，但他并不保证原子性。例如 volatile修饰 count，那么count++ 就不是原子的。  
2）AtomicIntegr 类提供的 getAndIncrement() 方法会原子性进行增量操作把当前值+1。  


+ CountDownLatch 和 CyclicBarrier区别和使用场景？
1）CountDownLatch：一个线程等待另外N个线程完成某件事之后才执行。countDown() 方法发出通知后，当前线程才可以执行。  
2）CyclicBarrier：N个线程相互等待，任何一个线程完成之前，所有线程必须等待。  
直到所有线程都准备好进入 await() 方法后，所有线程才开始执行。  
相同点或者不同点：  
3）CountDownLatch 和 CyclicBarrier 都能实现不同线程之间的等待，不过他们的侧重点不同，CountDownLatch 一般用于线程A等待若干线程执行完任务之后，它才执行。  
4）CountDownLatch不能够重用，CyclicBarrier能够重用。  


+ Semaphone 有什么用？  
1）信号量，限制某段代码块的并发数。  
2）Semaphone有一个构造函数，可以传入一个 int 型正数 n，表示某段代码最多只能够有 n 个线程访问到，如果超出了 n，那么请的等待，等到某个线程执行完毕，下一个线程再进入。  
sp.acquire() sp.release()  


+ happen-before原则有哪些？  
1）单线程内，写在前面的操作发生在后面的操作之前。  
2）unlock优先于同一个锁的 lock  
3)  volatile变量的写操作优先发生于读操作  
4）Thread 的 start 方法先执行于线程的其他操作  
5）线程中所有的操作都优先于线程的终止操作  
6）interrupt 方法的调用先发生于检测到中断事件的发生  
7）对象初始化完成优先于 finalize()  
8）A发生于B之前，B发生于C之前，A发生于C之前  


+ Copy-On-Write 是什么？  
即写时复制的容器，使用在读操作远多于修改操作的并发场景中，写时先将容器进行 Copy，复制出一个新的容器，然后新的容器里添加元素，添加完后，再将原容器的引用指向新的容器，是一种读写分离的思想，读和写不同的容器。