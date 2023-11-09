## 类型
vector              可变大小数组 可随机访问 尾部之外增删元素很慢
deque              双端队列 可随机访问 头尾增删元素快
list                    双向链表 可双向顺序访问 任意位置增删元素很快
forward_list      单向链表 可单顺序访问 任意位置增删元素很快
array                 定长数组 可快速随机访问 不能增删元素
string               类似于vector 专用于保存字符 随机访问快 尾部增删元素快 
<<<<<<< HEAD
/%/% (queue 队列 ， 好像在书上没有被提及，保留待查)
=======



>>>>>>> 8d1df998dcc6e1cac538dbfc1df898c1656a7b67
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
###### 通用操作
	a.swap(b);   | 交换a b的元素   swap不会移动元素，只交换两个容器的内部数
	swap(a,b);   | 据结构,原来的指针和引用不会失效(string 除外) 建议使用非成员版本
	c.size();          c中元素的数目(不支持forward_list)
	c.max_size();      c可以保存的最大元素数目
	c.empty();         c是否储存了元素，空返回true, 非空返回false

	resize不适应于array
	c.resize(n)        调整c的大小为n个元素,若n<c.size()则多出的元素被丢弃(指向被删除                                 元素的迭代器,引用,指针都会失效)若必须添加新元素,对新元素使用值初始化
	c.resize(n,t)      调整c的大小为n个元素.任何新添加的元素都初始化为值t

	shrink_to_fit只适用于vector,string,deque
	capacity和reserve只适用于vector和string
	c.shrink_to_fit()        请求将capacity()减少为于size()相同大小(退回不必要的内存空间)                                   (不保证一定退回内存空间)
	c.capacity()             不重新分配内存空间的话,c可以保存多少元素
	c.reserve(n)             分配至少能容纳n个元素的内存空间
[^reserve]

**添加删除**元素会改变容器大小对(array不适用)
	forward_list有专有版本的insert和emplace且不支持push_back和emplace_back
	vector和string不支持push_front和emplace_front

	c.push_back(t);           |
	c.emplace_back(args)；    |在c的尾部创建一个值为t或由args创建的元素
	
	c.push_front(t);          |
	c.emplace_front(args);    |在c的头部创建一个值为t或由args创建的元素

	c.insert(p,t);            |
	c.emplace(p,args);        |在迭代器p指向的元素之前床架你个值为t或者由args创建的元素，                                    返回新元素的迭代器
	c.insert(p,n,t);          在迭代器p指向的元素之前插入n个值为t的元素.返回指向新添加的第                                    一个元素的迭代器,若n=0返回P
	c.insert(p,b,e);          将迭代器b和e指定的范围内的元素插入到迭代器P指向的元素之前,b和e                                  不能指向c中的元素,返回新添加的第一个元素的迭代器,若范围为空返回p
	c.insert(p,il);           il是一个花括号包围的元素值列表.将这些给定值插入到迭代器P指向的元素                              之前.返回指向新添加的第一个元素的迭代器,若列表为空返回p


	forward_list有专有的erase且不支持pop_back,vector和string不支持pop_front
	c.pop_back();      删除c中尾元素
	c.pop_front();     删除c中首元素
	c.erase(p);        删除迭代器p所指元素,返回一个指向被删元素之后元素的迭代器,若p指向尾元素                           返回c.end()迭代器
	c.erase(b,e);      删除迭代器b和e所指定范围内的元素,返回一个指向最后一个被删元素之后的                              元素迭代器,若e本身为尾后迭代器(c.end())函数也返回c.end()
	c.clear();         删除c中所有元素

	不同容器下这些操作的接口不同:
	c.insert(args);       将args中的元素拷贝进c
	c.emplace(inits);     使用inits构造c中的一个元素
	c.erase(args);        删除args指定的元素
	c.clear();            删除c中的所有元素,返回void

###### 特殊的forward_list操作:
	对面forward_list其为单向链表不能进行前驱操作，其通过改变给定元素之后的元素来完成例如
	为了删除elem3用该用指向elem2的迭代器调用erase_after
	lst.before_begin();      返回指向链表首元素之前不存在的元素的迭代器(不能解引用).
	lst.cbefore_begin();     返回一个const类的lst.before_begin()返回的迭代器

	lst.insert_after(p,t);    |
	lst.insert_after(p,n,t);  |
	lst.insert_after(p,b,e);  |
	lst.insert_after(p,li);   |在迭代器p之后的位置插入元素.t是一个对象,n是数量,b和e是表示范围                                  的一堆迭代器(b,e不能指向lst内元素),il是一个花括号列表.返回一                                   个指向最后一个插入元素的迭代器,若范围为空,返回p,若p为尾后迭代                                   器则函数未定义.

	emplace_after(p,args);    使用args在p指定的位置之后创建一个元素.返回一个指向这个新元素的                                  迭代器

	lst.erase_after(p);       |
	lst.erase_after(b,e);     |删除p指向的位置之后的元素或删除从b之后直到(但不包含)e之间的元素                                返回一个指向被删元素之后元素的迭代器,若不存在这样的元素返回尾后                                 迭代器,如果p指向lst的尾元素或尾后迭代器函数未定义

###### string类的额外操作:
	构造:
	string s(cp,n);           s是cp指向的数组中前n个字符的拷贝,此数组至少包含n个字符
	string s(s2,pos2);        s是string s2从下标pos2开始的字符的拷贝,若pos2>s2.size()                                      构造函数未定义
	string s(s2,pos2,len2);   s是string s2从下标pos2开始的len2个字符的拷贝.若pos>s2.size()                                 构造函数未定义,不管len2值是多少，构造函数之多拷贝s2.size()-pos2                               个字符
	s.substr(pos,n)           返回一个string.包含s中从pos开始的n个字符的拷贝.pos的默认值为0.                                 n的默认值为s.size()-pos,即拷贝从pos开始的所有字符
	内容更改：
	s.insert(pos,args)        在pos之前插入args指定的字符.pos是一个下标或一个迭代器.接受下标的版本返回一个指向s的引用,接受迭代器的版本返回指向第一个插入字符的                                迭代器
	s.erase(pos,len)          删除从位置pos开始的len个字符.如果len被省略则删除从pos开始直至                                  s末尾的所有字符返回一个指向s的引用
	s.assign(args)            将s中的字符替换为args指定的字符.返回一个指向s的引用
	s.append(args)            将args追加到args,返回一个指向s的引用
	s.replace(range,args)     删除s中范围range内的字符,替换为args指定的字符,range或者是一个                                  下标和一个长度,或者是一对指向s的迭代器,返回一个之指向s的引用
		args(参数)可以是
		str              字符串
		str,pos,len      字符串,下标位置,长度
 		cp,len           从cp指向的字符数组的前(最多)len个字符
		cp               cp指向的以空字符结尾的字符数组
		n,c              n个字符c
		b,e              迭代器b和e指定的范围内的字符
		初始化列表        花括号包围的,逗号隔开的列表

	搜索:
<<<<<<< HEAD
	s.find(args)        查找s中args第一次出现的位置
	s.rfind(args)       查找s中args最后一次出现的位置
	s.
=======
	s.find(args)                查找s中args第一次出现的位置
	s.rfind(args)               查找s中args最后一次出现的位置
	s.find_first_of(args)       在s中查找args中任何一个字符第一次出现的位置
	s.find_last_of(args)        在s中查找args中如何一个字符最后一次出现的位置
	s.find_first_not_of(args)   在s中查找第一个不在args中的字符
	s.find_last_not_of(args)    在s中查找最后一个不在args的字符
	未找到返回npos 
	args必须为一下形式之一:
	c,pos       从pos位置(默认0)开始查找字符c
	s2,pos      从pos位置(默认0)开始查找字符串s2
	cp,pos      从pos位置查找指针cp指向的以空字符结尾的c风格字符串
	cp,pos,n    从pos位置开始查找指针cp指向的数组的前n个字符.pos和n无默认值

	比较:
	compare函数
	s.compare(args)
	args:
	s2                与s2比较
	pos1,n1,s2        从s的pos1处的n1个字符与n2比较
	pos1,n1,s2,pos2,n2     从s的pos1处的n1个字符与s2的pos2处的n2个字符比较
	cp                     比较s与cp指向的以空字符结尾的字符数组
	pos1,n1,cp             将s从pos1开始的n1个字符与cp指向的以空字符结尾的字符数组比较
	pos1,n1,cp,n2          将s从pos1开始的n1个字符与cp指向的地址开始的n2个字符比较

	转换:
	to_string(val)    返回val数值的string表示，是一组重载函数
	
	stoi(s,p,b)     
	stol(s,p,b)
	stoul(s,p,b)
	stoll(s,p,b)
	stoull(s,p,b)        返回s的起始子串(表示整数内容)的数值返回值类型分别是int, long,                                        unsigned long, long long, unsigned long long,   b表示                                            转换所用的基数默认为10.p是size_t指针保存s中第一个非数值字符的下标                                    ,p默认0即函数不保存下标 
	
	stof(s,p)
	stod(s,p)
	stold(s,p)
\>>>>>>> 168c5ce32090be03d4ba1da4a4942062ecf883c5
##### 关系运算符:
	==  !=              判断容器是否相等
	<  <=  > >=    如vector<char>以容器中不相等的第一个元素以字母顺序判断 (无序关联容器不支持)
**容器的关系运算符依照元素的关系运算符完成**

##### tips:
	1.使用对象初始化容器或者将一个对象插入时使用的是该对象的一个拷贝值.
	2.emplace函数直接在容器中构造元素.传递给emplace函数的参数必须于元素类型的构造函数想匹配即如果有c.emplace_back(int a, string b, bool c)的操作,emplace将这三个参数传递给c的元素类型构造函数直接构造(比如c是一个vector<struct_custom>，struct_custom这个结构体或类的构造函数包括这三个参数).
	3.程序员有责任保证所操作的元素是存在的
	4.向容器中添加删除元素操作可能会使指向容器元素的指针,引用,迭代器失效,需保证进行这些操作后正确定位迭代器
	5.注意resize改变的是元素数目,reserve改变的是容器容量

 

[^reserve]: reserve并不改变容器中元素的数量,仅影响vector预先分配多大内存空间,若此时c的需求大小大于当前容量 ,reserve至少分配所需求一样大的内存空间,若小于,什么都不做.

