## 类型
有序:
map                                                关联数组：关键字-值 对
set                                                   只保存关键字
multimap                                        关键字可重复出现的map
multiset                                           关键字可重复出现的set

无序:
unordered_map                             用哈希函数组织的map
unordered_set                                用哈希函数组织的set
unordered_multimap                     关键字可重复出现的unordered_map
unordered_multiset                       关键字可重复出现的unordered_set

头文件utility中的pair:
pair<T1,T2> p
p.frist和p.second分别指向p中的第一个和第二个元素, 其用关系运算符比较是用其元素的关系运算符来比较，且对两个元素的比较结果去交集返回比较结果
## 操作
key_type           关键字类型
mapped_type   只适用于map，关键字映射的类型
value_type        对于set与key_type相同 对于map返回pair<const key_type, mapped_type>

map的迭代器返回一个指向pair的引用  set的迭代器返回一个指向key_type 的const引用

插入:
c.insert()
c.emplace()   
参数为常见形式(类似泛型提供的操作)
对于不重复关键字的容器返回一个pair,frist是一个迭代器指向给定关键字的元素,second为bool指出是否插入或者已在其中

删除:
c.erase()

下标:
c[k]返回关键字为k的元素若无则添加

查找:
c.find(k)     返回第一个关键字为k的迭代器若无返回尾后迭代器
c.count(k)  返回关键字等于k的元素的数量,对于不重复关键字的容器返回0or1
c.lower_bound(k)
c.upper_bound(k)   不适用于无序容器，返回指向第一个不小于或大于k的元素的迭代器
c.equal_range(k)     返回一个迭代器pair表示关键字等于k的元素的范围，若不存在pair两个成员均为c.end()

bucket桶: