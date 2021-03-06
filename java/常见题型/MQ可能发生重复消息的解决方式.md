## MQ可能发生重复消息的解决方式

- 什么是MQ
- MQ的作用
- 重复消息是怎么回事？为何会产生重复消息
  1. 消息生产者把消息发给消息队列，是否接收到消息，生产者需要一个应答的(这里出问题，生产者未收到返回消息，就会重试)
  2. 消息队列收到消息后，因为负载高，相应变慢，当消息队列试图把消息发回给生产者的时候，生产者那边已经超时，又会发送
  3. 生产者发送消息后，生产者与消息队列之间的网络通讯出现问题了
  4. 消息从消息队列往消费者投递时产生了重复消息(消息队列给了消费者，但是消费者还没来得及应答消息队列，消息队列重试产生重复数据)
  5. 消息队列收到了消费者的应答，但是投递状态更新失败也会产生重复消息

![mq_process](../../image/mq_process.png)

- 重复消息带来的问题和如何解决重复消息

  解决重复消息采用幂等操作

  > update table_A set count = 10 where id = 1; //幂等
  >
  > update table_A set count = count + 1 where id = 1; //不幂等

  幂等操作有三种解决方式

  1. 乐观锁(消息在进行数据更新的时候带上数据的版本号，每个版本号只有一次执行成功的机会，如果失败生产者需要重新获取最新的版本号)
  2. 去重表，利用数据库表单的特性来实现去重（构建一个唯一性的索引），对于关系型有用