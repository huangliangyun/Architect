#### 问题

+ cookie 和 session 的区别？
+ BS与CS 的联系，还有区别？
+ 正则表达式及其用途？
+ Servlet的生命周期是什么样的？
+ 四种会话跟踪技术分别是什么？
+ Get 和 Post 区别？
+ JSP 和 Servlet 区别？
+ maven 命令？
+ 网站跨域问题产生的原因？
+ 什么是CDN内容分发？
+ 网站比较卡的原因？


#### 答案

+ cookie 和 session 的区别？
Cookie保存在客户端，容易被伪造，有传输限制为4k
Session保存在服务端，安全，没有大小限制


+ BS与CS 的联系，还有区别？
BS是浏览器服务器，CS是客户端服务器，BS的的客户端是浏览器，通过HTTP发送请求，CS 的架构可以是 PC，安卓，服务器可以想客户端主动发出信息。他们的硬件环境不同，安全要求不同，程序架构不同，系统维护不同。


+ 正则表达式及其用途？
主要用于过滤一些自定义规则的内容，常用场景如参数校验，爬虫等


+ Servlet的生命周期是什么样的？
类装载过程；init() 初始化过程；service() 服务过程，选择doGet \ doPost；destroy() 销毁过程。


+ 四种会话跟踪技术分别是什么？
url重写，隐藏表单域，cookie，seesion


+ Get 和 Post 区别？
1）get 是从服务器获取数据，post 是向服务器发送数据
2）get 通过地址传输，post 通过报文传输


+ JSP 和 Servlet 区别？
1）JSP编译后就会变成Servlet，JVM只能识别Java类，不能识别JSP代码，Web容器将 JSP 编译成JVM 能够识别的 Java 代码。
2）JSP本质是 Servlet 技术的扩展，是 Servlet 的简易实现，Servlet 的应用逻辑是在 Java 文件中。
3）JSP 是 Java 和 HTMl 组合成一个.jsp文件，JSP 侧重于视图，Servlet 侧重于逻辑控制。


+ maven 命令？
mvn compile 编译源码
mvn test-compile 编译测试
mvn test 运行测试
mvn package 打包
mvn install 在本地仓库安装jar
mvn clear 清除产生的编译wenjian
mvn source:jar 源码打包


+ 网站跨域问题产生的原因？
在微服务架构中，采用前后端分离技术，前端访问的域名端口和调用后端的域名和端口不一致造成的，这是浏览器的一种安全策略


+ 什么是CDN内容分发？
将静态资源缓存到全国各地各个节点，遵循就近访问原则，从而减少服务器的宽带传输


+ 网站比较卡的原因？
我们购买的云服务器宽带为1M，每秒最多传输 128kb 给客户端，如果一个页面有600kb，那么就需要5秒。
