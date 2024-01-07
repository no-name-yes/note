#### intro
ffmpeg是一个多元化的媒体转换器，可以支持任意数量的输入文件[^成对的映射]
转换流程图:
input file   -------demuxer(解调器)[^call]---->   encpded data packets   ------decoder----->   decoded frames   ------encoder------>   encouded data packets   ------muxer(复用器)------>   output file

当你使用stream copy时 ffmpeg会跳过解码编码阶段只进行demuxer和muxer,使用这种方式快速且品质没有损耗,但可能在一些情况中不能运行.



#### exmaple
转换一个输入文件到不同的格式 by re-encoding media streams:
ffmpeg -i input.avi outpu.mp4

将媒体视频的输出文件的比特率设置为64kbit/s
ffmpeg -i input.avi -b:v 64k -bufsize 64k output.mp4

强制将输出视频的帧率设置为24fps
ffmpeg -i input.avi -r 24 output.mp4

强制将输入文件的帧率设置为1fps(只能作用于原格式),并将输出文件的帧率设置为24fps:
ffmpeg -r 1 -i input.m2v -r 24 output.mp4

#### command synopsis 命令概要
ffmpeg [global_options]{[input_options] -i input_url}...{[output_opntions] output_url}


[^成对的映射]：在ffmpeg的命令中可以执行多对转换,但是所有的操作只能用于成对映射的输入输出文件,即0,1两个输入输出文件为一对,input_option和output_option作用于这一对作用域（可使用-map来选择流）

[^call]: 调用libavformat库

#### ffmpeg filtering
在编码之前,ffmpeg使用简易过滤器或复杂过滤器来处理原音频或者视频

详细过滤见官方文档[simple filtergragphs](https://ffmpeg.org/ffmpeg.html#toc-Simple-filtergraphs) [complex filtergraghp](https://ffmpeg.org/ffmpeg.html#toc-Complex-filtergraphs)