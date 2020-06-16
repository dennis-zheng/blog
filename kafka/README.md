本文主要分享kafka的consumer的消费机制，主要对以下关键点进行讲解：
* 同一topic，不同group id；
* 同一topic，同一group id；


# 1 同一topic，不同group id
同一topic，都会被不同group id的kafka_consumer消费;

## 1.1 启动
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/group_0.png)
启动两个kafka_consumer, 消费的主题都是"dennis-topic", 但加入的组不同，左边加入"dennis_group_0"组, 右边加入"dennis_group_1"组;

## 1.2 消费
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/group_1.png)
启动kafka_producer(图中下方), 生产一条信息，这时两个kafka_consumer都消费了这条消息;


# 2 同一topic，同一group id
同一topic，同一group id, 只被leader kafka_consumer消费;
当kafka_consumer有变动时(减少或增加)，就会重新选举leader(选举原理尚不明确);

## 2.1 启动一个consumer
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/same_group_0.png)
先启动一个kafka_consumer, 消费的主题"dennis-topic", 加入"dennis_group_0"组;

## 2.2 再启动一个consumer, 选举产生leader
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/same_group_1.png)
再先启动一个kafka_consumer(右边), 消费的同一主题"dennis-topic", 加入同一"dennis_group_0"组;
可以看出，左边与右边有点不同，倒数第二行"Updated partition assignment", 左边的方括号"\[\]"中有丰富内容，而右边的方括号中为空，即左边的kafka_consumer为leader;

## 2.3 消费
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/same_group_2.png)
启动kafka_producer(图中下方), 生产一条信息，这时只有左边的kafka_consumer(leader)消费了这条消息;

## 2.4 consumer选举leader
减少kafka_consumer
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/same_group_3.png)
强制终止左边的kafka_consumer(leader), 这时，右边有新的日志输出，显示重新推选leader，右边的kafka_consumer被选为leader;

增加kafka_consumer
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/same_group_4.png)
重新启动左边的kafka_consumer， 这时又重新推选leader, 左边的kafka_consumer被选为leader;

## 2.5 消费
![markdown](https://github.com/dennis-zheng/blog/blob/master/kafka/doc/same_group_5.png)
启动kafka_producer(图中下方), 生产一条信息，这时只有左边的kafka_consumer(leader)消费了这条消息;


# 3 问题
TODO ...