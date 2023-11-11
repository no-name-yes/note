![[Pasted image 20231111072531.png]]
tip:如上图的标记upd校验和还包括了一些ipv4的目的地址和源地址,这违反了分层原则

### UPD service model

unconnection datagram service(无连接)
self contained datagram(如果需要顺序需要对数据进行排序)
unreliable
	1.no ack
	2.no machanism to detect missing or mis-squenced datagram
	3.no flow control



