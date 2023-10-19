## 类型
vector              可变大小数组 可随机访问 尾部之外增删元素很慢
deque              双端队列 可随机访问 头尾增删元素快
list                    双向链表 可双向顺序访问 任意位置增删元素很快
forward_list      单向链表 可单顺序访问 任意位置增删元素很快
array                 定长数组 可快速随机访问 不能增删元素
string               类似于vector 专用于保存字符 随机访问快 尾部增删元素快 

### 操作

#### 常用
##### 类型别名：
	iterator 迭代器
	const_iterator 只能读元素不能进行写操作
	size_type 无符号整数类型，足够保存此种容器类型最大可能容器的大小
	difference_type 带符号整数类型，足够保存两个迭代器之间的距离
	value_type 元素类型
	reference 元素左值类型; 与value_type &含义相同
	const_reference const的reference

##### 构造:
	C c;             默认构造,孔容器
	C c1(c2);     构造c2的拷贝c1
	C c(b,e);      将迭代器b和e指定范围的元素拷贝到c（array不支持）
	C c{a,b,c...}; 列表初始化
	C c(n);        c包含n个值初始化的元素，此构造函数时explicit的(不支持string)
	C c(n,x);     初始化n个为x的元素
##### 赋值:
	c1=c2;           将c1中元素替换为c2中元素
	c1={a,b,c...};   将c1中元素替换为列表中元素
	顺序容器中的assign(不适用关联容器和array)
		c.assign(b,e);   将c中的元素替换为迭代器b和e范围中的元素,b,e不能指向c中                          的元素
		c.assign(il);      将c中的元素替换为初始化列表il中的元素
		c.assign(n,x);   将c中的元素替换为n个值为x的元素
		顺序容器中的assgin成员允许我们从一个不同但相容的类型赋值,或从容器的一个子序列赋值.assgin操作用参数所指定的元素(或拷贝)替换左边容器中的所有元素
		如将一个vector中的一段char* 值赋予一个list中的string:
			list<string> names;
			vector<const char*>oldstyle;
			name=oldstyle; // (X)容器类型不匹配
			names.assign(oldstyle.cbegin(),oldstyle.cend()); //(V)可以将const *char转换为string

##### 迭代器:
	c.begin(), c.end()      返回指向c的首元素和尾元素之后未知的迭代器
	c.cbegin(), c.cend()  只拥有写权限的c.begin(),c.end()
		反向容器的额外成员(不支持forward_list):
		reverse_iterator                按逆序寻址的迭代器
		const_reverse_iterator      不能修改元素的reverse_iterator
		c.rbegin(), c.rend()            返回指向c的为元素和首元素之前位置的迭代器
		c.crbegin(), c.crend()         只有读取限的c.rbegin(),c.rend()返回                                                                      const_reverse_iterator
	

##### 函数功能:
	a.swap(b);   | 交换a b的元素   swap不会移动元素，只交换两个容器的内部数
	swap(a,b);   | 据结构,原来的指针和引用不会失效(string 除外) 建议使用非成员版本
	c.size();          c中元素的数目(不支持forward_list)
	c.max_size();      c可以保存的最大元素数目
	c.empty();         c是否储存了元素，空返回true, 非空返回false
	
**添加删除**元素会改变容器大小对(array不适用)
	

	不同容器下这些操作的接口不同:
	c.insert(args);       将args中的元素拷贝进c
	c.emplace(inits);     使用inits构造c中的一个元素
	c.erase(args);        删除args指定的元素
	c.clear();            删除c中的所有元素,返回void

##### 关系运算符:
	==  !=              判断容器是否相等
	<  <=  > >=    如vector<char>以容器中不相等的第一个元素以字母顺序判断 (无序关联容器不支持)


 



