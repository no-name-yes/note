3 schemes of error detection: checksum ;  CRC ;  MAC


#### checksum
快速简单但检测功能弱不能检测两个bit改变

#### CRC
CRC(cyclic redundancy code)循环冗余检测码,多用于链路层校验，对于突发的bit改变检测效果好
可以检测小于c位的bit错误
CRC为[校验和](https://zh.wikipedia.org/wiki/%E6%A0%A1%E9%AA%8C%E5%92%8C "校验和")的一种，是两个字节数据流采用二进制除法（没有进位，使用[XOR](https://zh.wikipedia.org/wiki/XOR "XOR")来代替减法）相除所得到的余数。其中被除数是需要计算校验和的信息数据流的二进制表示；除数是一个长度为(n+1)的预定义（短）的二进制数，通常用多项式的系数来表示。在做除法之前，要在信息数据之后先加上n个0。

#### MAC(message authentication code)
现在常用，消息身份认证码
![[Pasted image 20231223104454.png]]


#### Quiz
Y or N to detect these that follows:

Algorithm          Single bit error  |  Run of 2 bit errors  |  Run of 9 bit errors  |  Two bit errors 100 bits apart 
8bit checksum             Y                         N                                 N                                         N
16bitchecksum            Y                         N                                 N                                         N
8bit CRC                      Y                         Y                                  N                                         N
16bit CRC                    Y                         Y                                  Y                                          N
32bit MAC                   N                        N                                 N                                          N