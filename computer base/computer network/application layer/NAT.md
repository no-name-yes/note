#### intro
NAT是一种地址转换协议，在现代的互联网中有许多设备都是基于ip网络协议来通信,其为越来越稀缺的ipv4地址提供了一种缓解方案. 也有安全和防火墙的功能(没有mapping之前只能从内往外发送信息),nat内的设备在没有mapping的情况下只能主动连接nat外的设备,无法被动接受(因为nat都过滤了)

nat是一种mapping,nat设备将在其后的私有ip地址和端口根据mapping表来转换为另一种地址
##### type of nat
数据包锥体抽象：
d ip          s ip
d port      s port
tip:此为nat收到要翻译给内网host的数据包,即从外接受到的数据包,在nat后的内部host发送packet都是将s ip 和 s port替换 下面锥体抽象为外部要经过nat发送给nat内部的packet,即d ip为nat ip,d port为nat port

full cone nat(全锥体)
d ip          
d port     
限制最小的一种类型,接受所有的tcp packet经过nat来进行mapping,只要目的ip和目的port存在mapping就进行转发,无论源ip和port(s ip and s port),位于nat后面的host可能丢弃返回icmp error

restricted cone nat(受限制锥体)
d ip          s ip
d port      
nat只将mapping表中地址相同,即nat从外接受到的packet中源地址(nat向外发出的包中目的ip地址一样的)进行限制,如ip一致则进行translate

port restricted cone nat(端口受限制的锥体)
d ip      s ip
d port  s port
nat不仅检测收到包的ip还检测port只有都一致时进行translate

symmetric nat(同步型)
不同的目的地不同的映射,有很大的复杂性较难管理

##### relay/hole-punching(中继,代理,转发,内网穿透)
当有设备处于nat后时,其它设备无法直接访问该设备(nat 中没有映射)此时需要一个代理服务,有nat后的设备在代理服务器上登记,并mapping,其它设备要访问nat之后的设备就有代理服务器转发请求,(*中继和打洞还是有区别的,打洞了之后就不再经由服务器了*)


##### operation detail
详细请见RFC文档
UDP RFC4787
TCP RFC5382