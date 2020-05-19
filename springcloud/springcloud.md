#### 问题
+ Spring Cloud 和 dubbo区别?
+ SpringBoot 和 SpringCloud 的区别？
+ Eureka、Zookeeper、Nacos 的区别？




#### 答案
+ Spring Cloud 和 dubbo区别?  
服务调用方式：Dubbo 是 RPC，SpringCloud 是 REST  
注册中心：Dubbo 是 Zookeeper，SpringCloud 是 Zookeeper 或者是 Eureka  
网关：Dubbo 没有，SpringCloud 有 Zuul，GateWay，还支持熔断器  


+ SpringBoot 和 SpringCloud 的区别？  
1）SpringBoot 专注开发单个个体微服务，SpringCloud 关注全局微服务治理  
2）SpringBoot 可以独立开发，SpringCloud 无法离开 SpringBoot  


+ Eureka、Zookeeper、Nacos 的区别？  
1) Eureka 是 AP，去中心化，每个节点都是相等的，采用你中有我，我中有你的相互注册思想，只要有一台 Eureka 节点存在，整个微服务就可以实现通讯。  
2) Zookeeper 采用 CP 保证数据一致性问题，原理是采用 ZAB 原子广播协议，如果 ZK 领导者出现了故障，就会进行选举领导者，选举的过程为了保证数据一致性问题，客户端无法使用 Zookeeper，所以整个微服务无法通讯。  
3) Nacos1.0 版本选择 AP 和 CP 混合实现注册中心，默认采用 AP，CP 采用 Raft 协议保持数据的一致性。  

