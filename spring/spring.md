#### 问题
+ @Controller 和 @RestController 的区别是什么？
+ Struts 拦截器和 Spring AOP 有什么区别？
+ Spring 中自动装配的方式有哪些？
+ 请问 Aop 的应用场景有哪些？
+ 事务传播机制？
+ 事务隔离级别？
+ Bean的生命周期？
+ SpringIOC 如何理解，底层原理？


#### 答案
+ @Controller 和 @RestController 的区别是什么？  
@RestController注解相当于@ResponseBody ＋ @Controller合在一起的作用  


+ Struts 拦截器和 Spring AOP 有什么区别？  
拦截器是AOP的一种实现，struts2 拦截器采用xwork2的interceptor！而spring的AOP基于IoC基础,其底层采用JDK动态代理与CGLIB两种方式结合的实现方式。  


+ Spring 中自动装配的方式有哪些？  
no：不进行自动装配，手动设置Bean的依赖关系。  
byName：根据Bean的名字进行自动装配。  
byType：根据Bean的类型进行自动装配。  
constructor：通过构造函数进行自动装配。   


+ 请问 Aop 的应用场景有哪些？  
日志记录，权限判断，异常统计和事务处理等  


+ 事务传播机制？  
1）Required：默认传播机制，如果外层有事务，当前事务加入外层事务，如果外层没有事务，则新建一个事务执行。  
2）Reques_new：每次开启一个事务，把外层事务挂起，当前事务执行完毕，恢复上层事务执行。如果外层没有事务，执行当前开启的事务即可。  
3）Support：如果外层有事务，则加入外层事务，如果外层没有事务，则直接以非事物执行，完全依赖外层事务。
4）Not_Support:不支持事务，如果外层存在事务就挂起，执行外当前代码，恢复外层事务，无论是否有异常都不会回滚当前代码。  
5）Never：不支持外层事务，如果外层有事务就抛出异常  
6）Mandatory：如果外层没有事务，则抛出异常  
7）Nested：保存状态，当前事务回滚到一个点，从而避免嵌套事务的回滚，及各自回滚各自的，如果子事务没有把异常吃掉，基本还会引起全部回滚。  


+ 事务隔离级别？  
Default：使用后端数据库默认隔离级别  
Read_Uncommitted:读未提交，可能导致脏读，幻读，不可重复读  
Read_Committed:读已提交，防止脏读，但可能会出现幻读和不可重复读  
Repeatable_Read：MySQL默认隔离级别，防止脏读和不可重复读，但仍会出现幻读  
Serializable:避免所有问题，但也是性能最慢的  


+ Bean的生命周期？  
1.首先进入Refresh方法，在这个方法里面会执行12个方法，prepareRefresh会进行一些准备的工作，obtainBeanFactory会得到实例化的工厂，prepareBeanFactory会对Bean工厂进行一些初始化的工作，postProcessBeaFactory为空的方法，然后是InvokeBeanFactoryPostProcessor，这里会对实现了BeanDefinitionRegisterPostProcessor，BeanFactoryPostProcessor这两个接口的类进行解析，其中，包括我们自定义的，也包括内部的，其中有一个类叫ConfigurationClassPostProcessor，首先会执行BeanDefinitionRegisterPostProcessor 里面的方法，这里会把我们加了注解扫描出来，然后放到一个BeanDefinitionMap里面，也就是我们定义Bean的模型，如果这个类加了@Configuration，就设置一个值为full，不是就判断是不是其余四种，如果是就设置为Lite。然后会执行BeanfactoryPostProcessor里面的方法，然后判断有没有Full类型的类，如果有，就添加CGLIB动态代理，生成一个属性$$beanFactory，当我们使用@Bean声明一个Bean的时候，如果@Bean方法调用了另一个@Bean方法，就会产生两个实例，违反了单例原则，这时候，添加了代理类，就会调用$$beanFactory直接去get，而不是又new一个。在完成Bean的扫描和注册之后，就会调用finishBeanFactoryInitialization对Bean进行实例化和初始化，然后调用getBean，dogetBean，然后两次调用getSingleton，doCreateBean,8次调用5个后置处理器对Bean进行实例化和初始化。
首先调用InstantionAwareBeanPostProcessor里面的postProcessorBeforeInstantiation方法，这个后置处理器继承了PostProcessor，内部提供了3个方法，加上BeanPostProcessor一共有5个方法，postProcessorBeforeInstantiation在目标对象实例化之前调用，该方法可以返回任何值，这个时候目标对象还没有被实例化，所以这个值可以代理本应该返回的对象，如果这个方法返回了一个值，接下来只会调用BeanaPostProcessor的postProcessorAfterInitialization方法，其他步骤不再执行，否则，按照正常流程走。
接着调用SmartInstantiationAwareBeanPostProcessor的determineCandidateConstructor方法，该方法主要是推断构造方法，继而实例化Bean，如果没有推断出来，使用默认的构造方法。
接着调用MergeBeanDefinitionPostProcessor的postProcessorMergeBeanDefinition，缓存Bean的注解信息。
接着调用SmartInstantiationAwareBeanPostProcessor的getEarlyBeanReference方法，提前暴露一个工厂，主要解决循环依赖的问题。
然后调用InstantiationAwareBeanPostProcessor的postProcessorAfterInstantiation方法，该目标方法在实例化之后调用，这时候对象已经被实例化了，但属性还没有被设置，如果该方法返回false，忽略属性的设置，如果返回false，按照正常流程走。
调用InstantiationAwarePostProcessor的postProcessorPropertyValue方法，对属性进行赋值和修改，如果postProcessorAfterInstantiation返回的值为false，该方法不执行。
调用BeanPostProcessor的postProcessBeforeInitialization方法和postProcessorAfterInitializayion方法，在这两个方法之间会执行生命周期的回调。


+ SpringIOC 如何理解，底层原理？  
控制反转，是一种开发思想，官网上说也是DI的另一种说法，在没有IOC之前，我们的对象由自己来创建和管理，IOC则是把对象的创建了管理都交给了这个容器。我们可以从微观和宏观的角度来理解IOC，从微观的调度来说，他底层就是一个SingletonObject，也就是一个单例池，宏观来说他是一种思想，一个工厂，甚至是一个艺术品，这个工厂由BeanDefinition，BeanFactoryPostProcessor，BeanPostProcessor等组件组成，并且有序巧妙地完成Bean的产生和管理这些Bean。