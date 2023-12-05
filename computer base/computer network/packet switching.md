

### history:
从以前的单个信号传递(烽火,信号塔)到更多的数据内容(信鸽,马匹等)等信息交换方式暴露出一些问题(消息拦截,篡改等)到现在的网络传输演变.
ciruit switching(电路交换)是现在分组交换(packet switching)的前身,电路交换主要用于电话通信,对于现代网络的数据量是太贫瘠的.

### delay:
end to end delay
	1.propagation delay(传播延迟)单个bit数据在l长的链路上传播的速度是c故其的传播延迟是t=l/c
	2.packetization delay(包延迟)传输整个数据包从第一个bit到最后一个bit所需要的时间,数据包大小p bit,传输方的输出速度为r bit/s,包延迟为t=p/r
	3.queueing delay(排队延迟) 这是不可预测,不确定的延迟,每比如每个路由器都有一个buffer,如果它buffer里的包很多,你的packet就需要进行排队等待其为不确定的Q(t)
故end to end的delay为t=$\sum_{}^{}$($\frac{l}{c}$+$\frac{p}{r}$+Q(t))

### match and action:(need to detect)
match有两种形式,一种是在以太网(交换机)上的匹配,一种是在英特网(网络路由器上的匹配).

match question:
以太网交换机:将目的IP地址匹配转发表取其中最长匹配前缀的路径转发到相应端口，如果表中没有任何匹配项则在其网段中广播
网络路由器:将目的IP地址匹配转发表的下一跳(hop)转发(tips:TTL会限制其发送次数，避免数据包可能在网络中无限循环的问题)


queue line congestion:
Q(t)不稳定的因素，根据网络情况而波动,line有很多种调度策略,如FIFO,优先级队列,加权优先级队列(可见相关联的operator system的调度方法)，在延时方面,可以根据传输速率和传输距离等除开Q(t)之外的条件算出固有延迟