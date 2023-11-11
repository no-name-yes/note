### ICMP service model
Reporting Message:  Self-contained message reporting error.
Unreliable: Simple datagram service - no retries.




ICMP(internet control message protocol)是一个简单的用于网络信息检测的协议,它将IP的8位有效负荷加上type和code来组成新IP数据包的data字段加上header发送

![[Pasted image 20231111081603.png]]






### ping command
ping指令发送一个type为8code为0的ICMP echo请求   目的host收到后恢复一个type0 code0的echo回复




### traceroute command
traceroute指令为检测网络中的路由经过情况，它返回各个路由器的经过，它发送一个由被封装了udp的ip报文段并将TTL设置为1在网络中由路由器对TTL递减至零返回一个type为11 TTL超时的ICMP报文,此时获取了到目的host的第一hop的信息,接下来source将TTL依次加一来检测下一跳直到目的host,目的host会返回一个prot unreachable的icmp，此时source直到到达了目的host，这个traceroute complete.