### intro
tcp不能控制传输中的中间传输过程，故而TCP实现的拥堵控制是通过调节报文中的Windows大小来控制的


#### AIMD
aimd(additive-increase/multiplicative-decrease)和性增长/乘性降低
IF packet received: W <-- W + $\frac{1}{W}$
IF packet is dropped: W <-- $\frac{W}{2}$
W:windows size 
[ainimation eaxmple] (http://guido.appenzeller.net/anims/)


#### thinking
