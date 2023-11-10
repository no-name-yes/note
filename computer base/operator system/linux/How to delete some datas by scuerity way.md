rm 指令 或者文件管理器删除文件只是删除指向文件系统的指针(inode)
	linux中文件由inode指针部分和data数据部分组成

主要要将还未被覆盖的数据使用新的数据来覆盖

可用shred ; dd 等指令来覆盖数据

> [Linux 中如何安全地抹去磁盘数据？ (qq.com)](https://mp.weixin.qq.com/s/w-pMU3_TD3dEPoW-XEde-A)