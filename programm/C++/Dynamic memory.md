### Why Dynamic memory
 - 1.程序不知道需要多少内存（容器类）
 - 2.程序不知道所需对象的准确类型（面向对象）
 - 3.程序需要在多个对象之间共享数据（常用）

静态内存和栈内存中的对象由编译器创建和销毁，动态分配的对象（运行时）储存在堆

使用new和delete来管理动态内存，需要确保销毁对象，否则会发生内存泄漏

使用shared_ptr和unique_ptr来自动释放内存，weak_ptr是一种伴随类，弱引用。其三都定义在memory头文件中,类似于vector，智能指针也是一种模板
如shared_ptr<string> p1

shared_ptr为一种共享动态指针，可以允许多个shared_ptr指向同一个对象
unique_ptr“独占”一个对象

对于shared_ptr独有的操作:

make_shared<T>(args) 返回一个shared_ptr 用(args)来初始化对象，如同顺序容器中的emplace一样用其元素T的构造函数来初始化

p.use_count() 返回与P共享对象的只能指针数量（可能很慢，主要用于调试）

p.unique()      若p.use_count()为1返回true否则返回false

对于shared_ptr有一个关联的计数器称为引用计数，当对shared_ptr进行拷贝时计数器递增，同样对shared_ptr销毁时计数器递减，当为0时自动释放内存

使用delete删除后可能会有空悬指针即指向一块无效内存的指针。如果要保留指针可以用nullptr赋值


