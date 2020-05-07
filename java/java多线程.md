#### 问题

+ 线程和进程区别？
+ 一个线程可以调用两次 start 吗？
+ 如何判断线程是否安全？
+ 为什么要用线程池？什么地方使用了线程池？
+ 线程的生命周期?
+ 线程池有哪些，特点，创建线程的方式？
+ 线程池有哪些方法，submit 和 execute 的区别?
+ 线程池的基本参数？
+ 怎么控制多个线程按序执行？
+ 线程池运行机制？
+ wait 和 sleep 区别？
+ stop 和 suspend 方法的区别？
+ notify 和 notifyAll 的区别？
+ 线程池和连接池区别？
+ 手写一个线程池？
+ Thread 和 Runnable 区别和联系？
+ Runnable 和 Callable 的区别？
+ final 不可变对象对多线程有什么帮助？
+ Java内存模型？


#### 答案


+ 线程和进程区别？  
1）进程是操作系统资源分配的基本单位，线程是任务调度和执行的基本单位  
2）同一个进程的线程共享该进程的地址空间，而进程之间则是独立的地址空间  
3）一个程序至少有一个进程，一个进程至少有一个线程   


+ 一个线程可以调用两次 start 吗？  
不可以，第二次调用会抛出异常。  


+ 如何判断线程是否安全？  
1）考虑原子性，可见性，有序性  
2）明确哪些代码是多线程运行的代码  
3）明确共享数据，对共享变量的操作是不是原子性，当某一个线程对共享变量进行修改的时候，对其他线程是可见的。  
4）对象是否会被多个线程访问修改，是的话是否有加锁操作。  


+ 为什么要用多线程？什么地方使用了多线程？  
1）复用线程，减少CPU的调度  
2）统一维护线程，提高程序的执行效率  
3）使用场景如AOP异步处理日志，异步发送短信，多线程下载  


+ 线程的生命周期? 
线程的生命周期分别为新建，就绪，运行，阻塞，死亡  
1）当我们调用 start 方法的时候线程由新建到就绪  
2）当线程获取到 CPU 资源的时候就会由就绪到运行状态  
3）当线程失去执行权就会由运行到就绪状态比如说调用 yield  
4）当运行时调用sleep，suspend，wait、join就会到阻塞状态  
5）当 sleep 时间到了或者调用 notify，notifyAll，resume 就会到达运行状态  
6）当执行完 run，调用stop，或者出现错误，或者出现异常没有处理线程就回到死亡状态。  


+ 线程池有哪些，特点，创建线程的方式？  
1）newCacheThreadPool() 处理大量短时间工作任务的线程池，试图缓存线程池并重用，如果没有线程池，就会创建线程池。如果闲置时间超过60秒，则被终止并移除缓存，长期闲置时，这种线程池不会消耗什么资源，内部使用SynchrousQueue作为工作队列。  
2）newFixThreadPool(int n)：重用指定数目的线程，背后是无界的工作队列，任何时候都有n个线程活动。意味着，如果超过了活动线程数目，将在工作队列中等待空闲线程出现。如果工作线程退出，将有新的工作线程被创建，以补足指定数目的线程数。  
3）newSingletonThreadExecutor():工作线程数限制为1，操作一个无界的工作队列，保证了所有任务都是被顺序执行，最多有一个任务处于活动状态，并且不允许使用者改变线程池的实例，因此可以避免改变线程池的数目。  
4）newSingleThreadSchduledExecutor() 和 newScheduledThreadPool(int n)创建的是ScheduleExecutorService，可以进行定时或者周期性的工作调度，区别在于单一线程还是多个线程。  
5）newWorkStealingPool() 可以并行处理任务，不保证顺序处理。  
https://www.cnblogs.com/gujiande/p/9488462.html    


+ 线程池有哪些方法，submit 和 execute 的区别?  
submit，execute，shutdown  
1）submit 底层还是调用了 execute，而是封装了一层 FutureTask  
2）submit 在执行的过程中与 execute 不一样，不会抛出异常，而是把异常保存在成员变量中，在FutureTask.get()阻塞获取的时候再把异常抛出。  
3）Spring 的 @Schedule 注解内部使用的就是 submit，如果你构建的任务内部有异常，你是永远也拿不到这个异常。  
4）execute 直接抛出异常后线程就死掉了，submit 保存异常线程没有死掉，因此 execute 的线程池可能会出现没有意义的情况，因为线程得不到复用，submit 不会出现这种情况。  
https://www.jianshu.com/p/29610984f1dd  


+ 线程池的基本参数？
1）corePoolSize：基本线程数量  
2）maximumPoolSize：最大线程数量  
3）keepAliveTime：空闲线程存活时间，当实际线程超过 corePoolSIze 时，若空闲时间超过该值，就会别停止。  
4）timeUnit：keepAlibeTime的 时间单位  
5）runnableTaskQueue：任务队列和大小，存放任务的阻塞队列  
ArrayBlckingQueue:数组实现，FIFO  
LinkedBlockingQueue：链表实现，FIFO，无界队列，newFixThreaPool  
SynchronousQueue：没有存储空间的阻塞度列，任务交给他之后必须交给一条工作线程处理，如果没有空闲工作线程，则创建一条新的工作线程，newCacheThreadPool  
PriorityBlockingQueue:优先权队列  
6）handler：饱和策略，实际线程达到 maximumPoolSize,并且队列已经满时，就会调用饱和策略。  
AbortPolicy：默认直接抛出异常  
CallerRunPolicy该任务被线程池拒绝，由调用 execute 方法的线程执行该任务；  
DiscardOldestPolicy：丢弃最老的一个，也就是马上要执行的一个任务；  
DiscardPolicy：丢弃当前任务  
https://www.jianshu.com/p/8ead5b396397  


+ 怎么控制多个线程按序执行？  
1、join  
2、newSingleThreadExecutor()  
https://www.cnblogs.com/coder-lzh/p/9404103.html  


+ 线程池运行机制？  
1）线程池实际线程数量小于corePoolSize，即使有空线程，即使有空线程，也会创建新的线程。  
2）当前线程的实际数量处于 corePoolSize 和 maxmumPoolSize 之间，如果队列没满，将任务放到阻塞队列。  
3）如果当前线程小于 maxmumPoolSize，阻塞队列满了，则直接创建线程处理任务。  
4）实际线程达到 maxmunPoolSize，阻塞队列也满了，使用饱和策略。  


+ wait 和 sleep 区别？
  1）wait 属于 Object 方法，sleep 属于 Thread 中的方法  
  2）wait 会让出 CPU 和释放锁资源，sleep 只会让出 CPU，不会释放锁资源  
  3）wait 只能在 synchronized 方法或者 synchronized s代码块中使用  

  4）唤醒  


+ stop 和 suspend 方法的区别？  
1）stop 是不安全的，他会解除由线程获取的所有锁定，而且如果对象处于一种不连贯的状态，那么其他线程能在那种状态下检查和修改他们，造成数据不一致。
2）suspend() 容易发生死锁，调用 suspend() 的时候，目标线程会停下来，但却仍然持有在这之前获得的锁。此时，其他线程都不能访问锁定的资源，除非被挂起的线程恢复运行。
  
+ notify 和 notifyAll 的区别？  
notify 只会唤醒一个线程，notifyAll 会唤醒所有的线程  


+ 线程池和连接池区别？  
线程池是一个容器，用来存放和管理线程;  
数据库连接池负责分配，管理，释放数据库连接，他允许程序使用一个现有的数据库连接，而不是重新建一个链接。  


+ 手写一个线程池？  
1）首先，我们需要定义一个集合，保存创建的线程  
2）然后定义一个阻塞队列，保存我们需要执行的任务  
3）在初始化的时候，我们先初始化指定数量的线程，执行start，然后把线程放到这个线程集合里面。  
4）如果阻塞队列不为空，我们就把任务拿出来，调用run方法执行  
5）我们可以定义一个execute 方法，把任务放到阻塞队列里面  


+ Thread 和 Runnable 区别和联系？  
1）Thread 是类，Runnable是接口  
2）Thread 底层实现了Rannable接口  
3）Runnable 可以实现资源共享，类实现了 Runnable 并不具备线程功能，必须通过new Thread(Runnable子类)调用 start 启动线程，所以我们通常通过 new Runnable 的子类启动多个线程解决资源共享问题。Thread 是类，所以每new一个对象的时候，资源已经被实例化了，不便实现资源共享。  
4）线程池只能放入 Runnable 和 Callable 类线程，不能直接放入继承 Thread 类线程。  
https://www.iteye.com/blog/zx-code-2220866  
https://blog.csdn.net/hd243608836/article/details/79946262  


+ Runnable 和 Callable 的区别？  
1）Callable 重写的方法是 call，Runnable 重写的方法是 run  
2）Callable 执行任务后可以返回值，Runnable 执行任务后不能返回值  
3）call 方法可以抛出异常，run 方法不能抛出异常  
4）运行 Callable 任务可以拿到一个 Future 对象，异步计算结果。他提供了检查计算是否完成的方法 isDone，以等待计算的完成。并检索计算的结果，通过 Future 对象可以了解任务的执行情况，可取消任务的执行，还可以获取执行结果。  


+ final 不可变对象对多线程有什么帮助？  
1）不可变对象保证了对象内存的可见性，对不可变对象的读取不需要而外的同步手段，提升了代码的执行效率。  
2）final 变量在并发中，是通过禁止 CPU 的指令重排序，保证了对象的内存可见性。  
3）final 能保证初始化过程的安全性，保证正在创建中的对象不能被其他线程访问到。比如静态内部类的单例模式。


+ Java内存模型？
1）JMM 定义了多线程之间共享变量的可见性。
2）JMM 内部通过内存屏障实现，通过禁止重排序，保证内存的可见性，也就是各种 happen-before 原则。
3）抽象上来看，JMM 定义了线程和主存之间的抽象关系，线程之间共享变量存储在主内存中，每个线程都有一个私有的本地内存，本地内存中存储了该线程读写共享变量的副本。
4）与 JVM 不同，JMM 定义了 Java 虚拟机 JVM 在计算机内存中的工作方式，JVM 是整个计算机的模型，JMM 是隶属于 JVM 的。







