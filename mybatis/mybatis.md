#### 问题

+ MyBatis 简介？
+ mybatis 的 #{} 和 ${} 区别 ？
+ 请简述一下Mybatis和Hibernate的区别是什么？
+ 一级缓存和二级缓存？


#### 答案

+ MyBatis 简介？
Mybatis是一种半自动的ORM框架，程序员需要自己编写SQL语句，开发方便。使用的时候，首先，我们需要使用 @MapperScan 扫描数据接口层的包，我们可以使用注解方式或者 xml 方式实现 SQL语句，一般我们开发的时候都使用 xml 方式，xml里面有个 namespace 属性就是我们所定义的接口的包路径。


+ mybatis 的 #{} 和 ${} 区别 ？
${} 属于字符串替换，也可以对传递的参数拼接到 SQ L中
#{} 会将 SQL 中的 #{} 替换为？号，在 SQL 执行前会使用 PrepareStatement 的参数设置方法，按序给SQL的？占位符设置值参数。所以#{}是预编译的，有效防止SQL注入，提高系统安全性


+ 请简述一下Mybatis和Hibernate的区别是什么？
MyBatis是一种半自动ORM框架，是对象关系映射，需要手写SQL，比较灵活
Hiberate是一种全自动ORM框架，操作简单开发快，对SQL的修改和优化比较困难


+ 一级缓存和二级缓存？  

  一级缓存   

  1、一级缓存是基于SqlSession级别，默认开启，在对象中有一个HashMap用于存储缓存数据，使用[namespace+sql+参数]作为key，HashMap是当前会话私有的，其他的SqlSession无法访问。  
  2、如果SQLSession执行DML操作，并commit，mybatis就会清空当前缓存中的所有缓存数据，保证缓存中的数据和数据库中的一致，避免出现脏读。  
  3、在集群的情况下，由于每个SQLSession有自己独立的缓存，所以会造成数据冲突。  
  4、Spring整合MyBatis  
  1)如果没有开启事务，每次查询，Spring都会关闭旧的SqlSession，创建新的SqlSession,此时一级缓存没有作用。 
  2）在开启事务的情况下Spring使用ThreadLocal获取当前资源绑定的同一个SqlSession，因此一级缓存有效。  
  https://blog.csdn.net/pange1991/article/details/81391715    
  
  二级缓存  
  1、二级缓存是跨SqlSession的，是 namespace 级别的缓存，多个 SqlSession 操作同一个 Mapper 的语句。  
  2、所以在多表查询的时候，极大可能出现脏读数据，在分布式环境下，默认的 MyBatis 缓存都是基于本地的，必然   会出现脏读，所以使用像 Redis 等分布式缓存成本更低，安全性更高。  
  3、开启缓存  
  https://www.cnblogs.com/charlypage/p/9747145.html