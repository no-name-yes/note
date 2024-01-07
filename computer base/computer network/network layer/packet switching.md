

### history:
从以前的单个信号传递(烽火,信号塔)到更多的数据内容(信鸽,马匹等)等信息交换方式暴露出一些问题(消息拦截,篡改等)到现在的网络传输演变.
ciruit switching(电路交换)是现在分组交换(packet switching)的前身,电路交换主要用于电话通信,对于现代网络的数据量是太贫瘠的.

### delay:
end to end delay
	1.propagation delay(传播延迟)单个bit数据在l长的链路上传播的速度是c故其的传播延迟是t=l/c
	2.packetization delay(包延迟)传输整个数据包从第一个bit到最后一个bit所需要的时间,数据包大小p bit,传输方的输出速度为r bit/s,包延迟为t=p/r
	3.queueing delay(排队延迟) 这是不可预测,不确定的延迟,每比如每个路由器都有一个buffer,如果它buffer里的包很多,你的packet就需要进行排队等待其为不确定的Q(t)
故end to end的delay为t=$\sum_{}^{}$($\frac{l}{c}$+$\frac{p}{r}$+Q(t))

### switching:
switching有两种形式,一种是在以太网(交换机)上的匹配,一种是在英特网(网络路由器上的匹配).

![[Pasted image 20231207092628.png]]

Ethternet switching and router switching:
以太网交换机:将目的IP地址匹配转发表取其中最长匹配前缀的路径转发到相应端口，如果表中没有任何匹配项则在其段口中广播
以太网交换的转发表以哈希储存(也可能有其它方式如双哈希(two-way hash)增加第一次命中率,)


网络路由器:检测Ethernet DA即以太网目标地址是否属于该路由器是,接受否则丢弃,接着检测IP版本和数据帧长度,接下来减少TTL,update checksum(checksum包括TTL) 查看TTL是否为0,查找转发表将其转发至正确的端口,找到下一跳路由器的Ethernet DA,将其封装进一个新的Ethernet frame(帧)发送

网络交换的转发表的lookup(查找匹配)是找出匹配的具有最长的前缀匹配行;最长前缀匹配可用二叉树来实现,考虑32位ip地址,因为前缀匹配的长度不同,那么所存储的叶子节点的度就是不同的,使用mask掩码机制来表示32位中的有效位,比如转发表中的一个匹配项位120.0.0.0/24即前8位为有效前缀匹配,前缀匹配为01111000那么使用掩码机制为11111111后加上24为0,其中1表示有效位数,0表示无效位数.


Ethernet switches 和 router switches 都对包交换做两个动作,从转发表中查找匹配地址->交换数据包到正确的出口,即匹配加转发(matching and forwording)


queue line congestion:
Q(t)不稳定的因素，根据网络情况而波动,line有很多种调度策略,如FIFO,优先级队列,加权优先级队列(可见相关联的operator system的调度方法)，在延时方面,可以根据传输速率和传输距离等除开Q(t)之外的条件算出固有延迟