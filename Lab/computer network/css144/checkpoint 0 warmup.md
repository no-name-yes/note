## lab 0
1.fetch a web page
		使用telnet cs144.keithw.org http命令链接到远程服务器
		再输入：
			```
			GET /hello HTTP/1.1
			Host: cs144.keithw.org
			Connection: close
			```
		Assigment:从http://cs144.keithw.org/lab0/sunetid中获取信息如下
			HTTP/1.1 200 OK
			Date: Tue, 10 Oct 2023 08:03:34 GMT
			Server: Apache
			X-You-Said-Your-SunetID-Was: sunetid
			X-Your-Code-Is: 826854
			Content-length: 111
			Vary: Accept-Encoding
			Content-Type: text/plain
		Hello! You told us that your SUNet ID was "sunetid". Please see the          HTTP headers (above) for your secret code.
		将请求地址中http://cs144.keithw.org/lab0/sunetid的sunetid换为从响应报文中      的数据发送
		以上也可直接使用crul命令来实现

2.send yourself an email
		这个smtp通信要求与stanford服务器连接 在进行RCPT TO接收方的邮件地址填写时会有unknow user的问题(用的前一个的unetid)，这里用其它的smtp服务器地址。[^1]
		这里我telnetgmail的smtp服务器超时用谷歌服务器
		![[Pasted image 20231017153359.png]]

		此时新创建的阿里云邮箱也已经收到信息了
![[Pasted image 20231017153521.png]]

2.3 Listening and connecting
		使用netcat -v -l -p 9090 打开对9090端口的监听
		打开一个新的会话 使用telnet localhost 9090来连接到本地9090端口
		发送信息即可通信

3 writing a nework program using an OS stream
		git clone https://github.com/cs144/minnow 指令来获得nodebase

	writing webget 
	补充所克隆仓库minnow中的webget.cc文件在其中的get_url函数中补充代码完成以代码的形式向网站发送报文。
	编写一个webget的C++套接字程序,你只需在webget.cc里面的get_url函数中补充缺少的部分,现在来考虑tcp的连接过程,作为一个cilent我们需要向一个服务区发送我们的请求,接下来我们需要将我们请求的内容写入报文段发送给接收方，紧接着我们只需要读取回复的报文即可，首先我们要生成socket.hh头文件中提供的tcpsocket类,让后绑定一个地址和提供使用的协议,再使用tcpsocket的write函数写入报文发送

	其中补充的代码如下:
![[Pasted image 20231113194200.png]]

[[TCP FSM]]
让我们考虑一下tcp fsm的流程,首先考虑到服务器已经处于监听状态,我们的客户机处于closed状态,现在我们需要实例化一个tcpsocket,对其绑定地址和使用的协议,此时与服务器去建立tcp连接,再用write函数去写入字符串报文tcp会将其发送给服务器,再使用一个字符串s缓冲接收回复的报文段当读入EOF(end of file)时完成。输出打印报文结果.使用指令./apps/webget cs144.keithw.org /hello测试结果如下:
![[Pasted image 20231113195449.png]]

minnow中还有两个测试用例输入cmake --build build --target check_webget来测试使用单元
![[Pasted image 20231113195806.png]]



An in-memory reliable byte stream 
现在你需要在内存中实现可靠,有序,流控制,有限的字节流传输。尽管internet提供的只是尽最大努力的交付传输,现在有输入和读取两方,在byte_stream.hh和byte_stream.cc中实现以下接口:
writer:


```cpp
 void push( std::string data ); // Push data to stream, but only as much as available capacity allows.

  void close();     // Signal that the stream has reached its ending. Nothing more will be written.
  void set_error(); // Signal that the stream suffered an error.

  bool is_closed() const;              // Has the stream been closed?
  uint64_t available_capacity() const; // How many bytes can be pushed to the stream right now?
  uint64_t bytes_pushed() const;       // Total number of bytes cumulatively pushed to the stream
```


reader:
```cpp
 std::string_view peek() const; // Peek at the next bytes in the buffer
  void pop( uint64_t len );      // Remove `len` bytes from the buffer

  bool is_finished() const; // Is the stream finished (closed and fully popped)?
  bool has_error() const;   // Has the stream had an error?

  uint64_t bytes_buffered() const; // Number of bytes currently buffered (pushed and not popped)
  uint64_t bytes_popped() const;   // Total number of bytes cumulatively popped from stream
  ```

补充的代码如下:




使用指令cmake --build build --target check0来测试本例。





[^1]:
	1. 阿里云邮箱(mail.aliyun.com):
	POP3 服务器地址:pop3.aliyun.com(SSL加密端口：995；非加密端口：110)
	SMTP 服务器地址:smtp.aliyun.com(SSL加密端口：465；非加密端口：25)
	IMAP 服务器地址：imap.aliyun.com(SSL加密端口：993；非加密端口：143)
	1. 谷歌邮箱(google.com)：
	POP3 服务器地址:pop.gmail.com(SSL启用端口：995)
	SMTP 服务器地址:smtp.gmail.com(SSL启用端口：587)
	1. 新浪邮箱(sina.com):
	POP3 服务器地址:pop3.sina.com.cn(端口：110)
	SMTP 服务器地址:smtp.sina.com.cn(端口：25)
	1. Tom邮箱(top.com):
	POP3服务器地址:pop.tom.com(端口：110)
	SMTP服务器地址:smtp.tom.com(端口：25)
	1. 网易邮箱(163.com):
	POP3 服务器地址:pop.163.com(端口：110)
	SMTP 服务器地址:smtp.163.com(端口：25)
	1. 126邮箱:
	POP3服务器地址：pop.live.com(端口：995)
	SMTP服务器地址:smtp.126.com(端口：25)
	1. 雅虎邮箱(yahoo.com):
	POP3服务器地址:pop.mail.yahoo.com
	SMTP服务器地址:smtp.mail.yahoo.com
	1. 雅虎中国(yahoo.com.cn):
	POP3服务器地址:pop.mail.yahoo.com.cn(端口：995)
	SMTP服务器地址:smtp.mail.yahoo.com.cn(端口：587)
	雅虎邮箱POP3的SSL不启用端口为110，POP3的SSL启用端口995；SMTP的SSL不启用端口为25，SMTP的SSL启用端口为465。
	1. Foxmail邮箱(foxmail.com)：
	POP3服务器地址:POP.foxmail.com(端口：110)
	SMTP服务器地址:SMTP.foxmail.com(端口：25)
	1. QQ邮箱(mail.qq.com)
	POP3服务器地址：pop.qq.com(端口：110)
	SMTP服务器地址：smtp.qq.com(端口：25)
	SMTP服务器需要身份验证。
	1. 搜狐邮箱(sohu.com):
	POP3服务器地址:pop3.sohu.com(端口：110)
	SMTP服务器地址:smtp.sohu.com(端口：25)
	1. HotMail邮箱(hotmail.com)：
	POP3服务器地址：pop.live.com(端口：995)
	SMTP服务器地址：smtp.live.com(端口：587
	1. 移动139邮箱:
	POP3服务器地址：POP.139.com(端口：110)
	SMTP服务器地址：SMTP.139.com(端口：25)
	1. 中华网邮箱(china.com):
	POP3服务器地址:pop.china.com(端口：110)
	SMTP服务器地址:smtp.china.com(端口：25)
	以上信息来自网站：https://blog.51cto.com/aiyc/3115045

