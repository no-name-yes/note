### Why Dynamic memory
 - 1.程序不知道需要多少内存（容器类）
 - 2.程序不知道所需对象的准确类型（面向对象）
 - 3.程序需要在多个对象之间共享数据（常用）

静态内存和栈内存中的对象由编译器创建和销毁，动态分配的对象（运行时）储存在堆

使用new和delete来管理动态内存，需要确保销毁对象，否则会发生内存泄漏

使用shared_ptr和unique_ptr来自动释放内存，weak_ptr是一种伴随类，弱引用[^weak_ptr]。其三都定义在memory头文件中,类似于vector，智能指针也是一种模板
如shared_ptr<string> p1

shared_ptr为一种共享动态指针，可以允许多个shared_ptr指向同一个对象

shared_ptr的操作:
shared_ptr<T> p(q,d)      p接管了内置指针q所指向的对象的所有权.q必选转换为T*类型，同时p将使用可调用对象d来代替delete

shared_ptr<T> p(p2,d)    p是shared_ptr p2的拷贝，p使用可调用对象d来代替delete

p.reset()
p.reset(q)
p.reset(q,d)     若p是唯一指向其对象的shared_ptr,reset会释放此对象，若有可选参数内置指针q,则令p指向q,否则p置空，若还有d则会使用可调用对面d而不是delete来释放q.


unique_ptr“独占”一个对象

对于shared_ptr独有的操作:

make_shared<T>(args) 返回一个shared_ptr 用(args)来初始化对象，如同顺序容器中的emplace一样用其元素T的构造函数来初始化




p.unique()      若p.use_count()为1返回true否则返回false

对于shared_ptr有一个关联的计数器称为引用计数，当对shared_ptr进行拷贝时计数器递增，同样对shared_ptr销毁时计数器递减，当为0时自动释放内存

使用delete删除后可能会有空悬指针即指向一块无效内存的指针。如果要保留指针可以用nullptr赋值

智能指针还有定义了一个get函数，其返回一个内置指针，指向智能指针管理的对象,get用来将指针的访问权限传递给代码，你只有在确定代码不会delete指针的情况下，才能使用get，特别是不要使用get初始化另一个智能指针或者为另一个智能指针赋值.


#### allocator
同样被包含在头文件memory中的库函数，在使用new这种动态内存分配的函数时，内存的调配和构造是一同进行，而使用allocator可只分配内存不进行构造(?)






[^weak_ptr]:

