#### 问题

+ MyBatis 简介？
+ mybatis 的 #{} 和 ${} 区别 ？
+ 请简述一下Mybatis和Hibernate的区别是什么？


#### 答案

+ MyBatis 简介？
Mybatis是一种半自动的ORM框架，程序员需要自己编写SQL语句，开发方便。使用的时候，首先，我们需要使用 @MapperScan 扫描数据接口层的包，我们可以使用注解方式或者 xml 方式实现 SQL语句，一般我们开发的时候都使用 xml 方式，xml里面有个 namespace 属性就是我们所定义的接口的包路径。


+ mybatis 的 #{} 和 ${} 区别 ？
#{} 对传入的参数会进行预编译，${} 不会预编译，传过来是什么就是什么。


+ 请简述一下Mybatis和Hibernate的区别是什么？
MyBatis是一种半自动ORM框架，是对象关系映射，需要手写SQL，比较灵活
Hiberate是一种全自动ORM框架，操作简单开发快，对SQL的修改和优化比较困难
