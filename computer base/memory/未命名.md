

在一个为8G(gigabytes)[^gigabytes](约为2的32次方)的内存中，



[^gigabytes]:约为2的30次方


#### Endianness(字节序)

假如计算机可以在内存中读取连续的8byte(64bit)字节单元来加载64位整二进制整数(单字节为0~256)，当超过1byte的数要被读取时需要读取更多的字节单元，比如可以表示1024(2的10次方)需要大于1byte(8bit)即需要2byte(16bit)(实际需要10bit),此时需要布置多字节(字节序)。

1024 = 0x0400
##### little endian
最低有效字节最先出现
address0    address1
0x00           0x04
从架构角度来看很有意义

##### large endian
最高有效字节先出现
address0    address1
0x04           0x00
从左到右符合阅读顺序