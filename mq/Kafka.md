#### 问题
+ Kafka如何保证消息顺序？
+ Kafka节点如何相互感知？
+ Kafka如何保证高吞吐量？
+ Kafka 内部原理？工作流程？
+ Kafka 怎么保证数据可靠性？有什么优缺点？


#### 答案

+ Kafka如何保证消息顺序？  
顺序问题的背景：  
1）单个 Broker 的情况下，存放消息默认情况下是有序的，因为遵循队列的先进先出原则。  
2）如果投递的消息行为是一样的情况下，没有必要关注消息顺序性问题。  
3）Broker 是集群的情况下，消息存放到了不同的分区，如果生产者往同一个队列中存放消息行为不统一，存在消息顺序性问题。如 insert->update->delete 。  
4）生产者，消费者异步的情况下  
如何解决：  
对相同业务逻辑的消息设置相同的消息 key，存放到同一个 Broker 中  


+ Kafka节点如何相互感知？  
注册到同一个Zookeeper，使用事件监听相互感知  


+ Kafka如何保证高吞吐量？  
1.顺序读写(kafka 的消息是不断追加到文件中的，这个特性使 kafka 可以充分利用磁盘的顺序读写性能)  
2.零拷贝(就是跳过用户缓冲区，直接从内核到内核再到网卡，省去了用户空间的复制)  
3.分区(kafka 中的 topic 中的内容可以被分为多分 partition 存在,每个 partition 又分为多个段segment,所以每次操作都是针对一小部分做操作)  
4.批量发送(kafka 允许进行批量发送消息，producter 发送消息的时候，可以将消息缓存在本地,等到了固定条件发送到 kafka)  
5.数据压缩(Kafka 还支持对消息集合进行压缩，Producer 可以通过 GZIP 或 Snappy 格式对消息集合进行压缩)  
https://www.cnblogs.com/barrywxx/p/11544379.html  


+ Kafka 内部原理？工作流程？  
kafka 依赖于 Zookeeper，一个 kafka 节点就是一个 Broker，一类的消息成为 Topic，Kafka 集群能够同时负责多个Topic 的分发，一个 Topic 在物理上可以分为多个 Partition，每个 Partition 是一个有序的队列，相当于 redis 集群中的卡槽，一个 Partition 物理上由多个 Segment 组成，存储着Message。生产者在投放消息的时候会传递 key，根据 key 计算 Hash 值确定投放在哪个 Broker中。


+ Kafka 怎么保证数据可靠性？有什么优缺点？  
基于领导者的副本机制  

