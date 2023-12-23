### end to end principle
如果想要数据准确的传送要使用端到端原则，比如tcp可以准确的传输数据而不需要链路层的帮助(但是链路层的帮助可以提供tcp的性能),如果让链路层来执行准确传输检测error可能在某个点发生错误。**简而言之就是网络可以提供各种帮助,但也只是帮助,你不能依赖它.**  



>(”strong“ end to end principle”强“端到端原则)[^1]The network's job is to transmit datagrams as efficiently and flexibly as possible. Everything else should be done at the fringes...            -[RFC 1958]


[^1]:其中弱端到端原则是可以在中间实现一些端到端的东西来提升性能,强端到端的原则则是要求在不能在中间实现