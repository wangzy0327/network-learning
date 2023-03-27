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