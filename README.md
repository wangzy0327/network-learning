# 计算机网络

网络数据包格式

![network-package-format](imgs/network-package-format.png)

网络包大小

Maximum Transmission Unit（MTU）= IP Header + TCP Header + MSS

Maximum Segmant Size（MSS）= MTU - IP Header - TCP Header

![package-size](imgs/package-size.png)

tcp头部

![tcp-header](imgs/tcp-header.png)

udp头部

![udp-header](imgs/udp-header.png)

TCP三次挥手

![tcp-three-shake](imgs/tcp-establish.png)

TCP四次挥手

Maximum Segment Lifetime （MSL），报文最大生存时间

IP Header里面的TTL字段，一般为64，Linux将MSL设置为30秒。

![tcp-four-waving](imgs/tcp-fin.png)

TCP作为一个面向连接的、可靠的传输协议，内部实现了一个**重传计时器**来保证数据能传输到对方。每发送一个数据包，就给这个数据设置一个重传计时器。如果在计时器超时之前收到了针对这个数据包的ack，就取消这个计时器。如果没有收到，则开始发起重传。计时器超时的时间被称为RTO，这个时间的确定取决于RTT

关于两者详细的解释：

- `RTT(Round Trip Time)`：一个连接的往返时间，即数据发送时刻到接收到确认的时刻的差值；
- `RTO(Retransmission Time Out)`：重传超时时间，即从数据发送时刻算起，超过这个时间便执行重传

对于segment的重传，重传的时间RTO设定是非常重要的，如果设置太短，可能会导致并没有丢包而重传，如果设置太长了，可能因为等待ACK而浪费掉很多时间，牺牲传输的效率。从思想上来讲，其实我们还是希望重传的时间需要稍稍的大于RTT就可以了。但是这个RTT没有什么可以使用的定值，它是不断变化的
注意建立TCP三次握手的超时重传跟传输segment的重传次数跟时间不同。

在Ubuntu18.04下，tcp的syn重传次数为6次，其中第一次重传时间为1s，第二次为2s，依次指数增长

```shell
cat /proc/sys/net/ipv4/tcp_syn_retries
6
```

![syn-retry](imgs/syn_retry.png)

