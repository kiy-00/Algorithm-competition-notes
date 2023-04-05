# STL的使用


---



## String

---

```c++
string s="abcde";
s.begin();
s.end();
s.rbegin();
s.rend();
s.front();
s.back();
s+="aaa";
s+='a';
s.push_back('a');
s.pop_back();
s.insert(s.begin(),'?');
//s="?abcde"
s.insert(0,"fff");
//s="fffabcde"
s.insert(5,"fff")
//s="abcdefff"
s.insert(5,3,'f');
//s="abcdefff"
s.erase(s.begin()+3,s.begin()+4);
//s="abce"
s.erase(0,4);
//s="e";
char t[]="12345";
s.copy(t,2,3);
//s="abcde";
//t="de345";
s.find('c')=2;
s.append("abcde");
//s="abcdeabcde";
s.rfind('c')=7;

s.append("abcde");
//s="abcdeabcde";
s.find_first_of('c')=2;
s.find_last_of('c')=7;

s="012345678";
string t=s.substr(3);
//t="345678";
string tt=s.substr(0,4);
//tt="0123";

string s="12345";
int t=stoi(s);
//t=12345，如果有前导零、非法字符等会出错
//注意转化的数字范围不能超过int、long long等

string s="123.45";
double t=stod(s);
//t=123.45

//除此之外还有stol,stoll,stoul,stoull等
int t=23423;
string s=to_string(t);
//s="23423";

double t=333.23;
string s=to_string(t);
//s="333.230000",默认是六位小数







```







## 序列式容器：

---


```c++
vector<int> data(10);

for (int i = 0; i<data.size(); i++)
	cout << data[i] <<endl;

for (vector<int>::iterator iter = data.begin(); iter != data.end(); iter++)
	cout << *iter << endl;
	
auto iter = data.begin();

```

```c++
∕∕ 1. 创建空 vector; 常数复杂度
vector<int> v0;
∕∕ 1+. 这句代码可以使得向 vector 中插入前 3 个元素时，保证常数时间复杂度
v0.reserve(3);
∕∕ 2. 创建一个初始空间为 3 的 vector，其元素的默认值是 0; 线性复杂度
vector<int> v1(3);
∕∕ 3. 创建一个初始空间为 3 的 vector，其元素的默认值是 1;
vector<int> v2(3, 2);
∕∕ 4. 创建一个初始空间为 3 的 vector，其元素的默认值是 2， 线性复杂度
∕∕ 并且使用 v2 的空间配置器; 线性复杂度
vector<int> v3(3, 1, v2.get_allocator());
∕∕ 5. 创建一个 v2 的拷贝 vector v4，其内容元素和 v2 一样; 线性复杂度
vector<int> v4(v2);
∕∕ 6. 创建一个 v4 的拷贝 vector v5，其内容是 {v4[1], v4[2]}; 线性复杂度
vector<int> v5(v4.begin() + 1, v4.begin() + 3);
∕∕ 7. 移动 v2 到新创建的 vector v6，不发生拷贝; 常数复杂度; 需要 C++11
vector<int> v6(std::move(v2)); ∕∕ 或者 v6 = std::move(v2);

```

## 关联式容器：

---


### set

set 是关联容器，含有键值类型对象的已排序集，==搜索、移除和插入拥有对数复杂度==。 set 内部通常采用==红黑树==实现。平衡二叉树的特性使得==set非常适合处理需要同时兼顾查找、插入与删除的情况==。
和数学中的集合相似, ==set中不会出现值相同的元素。如果需要有相同元素的集合，需要使用multiset。==

multiset的使用方法与set的使用方法基本相同。

---


![image-20230112111045672](C:\Users\yi'k\AppData\Roaming\Typora\typora-user-images\insert函数的返回值.png)



![image-20230112110930774](C:\Users\yi'k\AppData\Roaming\Typora\typora-user-images\set支持的操作.png)



==lower可以等于，upper不可以等于==



---


### map

搜索、移除和插入操作拥有==对数复杂度==。map通常实现为红黑树。map重载了operator[]，可以用任意定义了operator<的类型作为下标（在map中叫做key，也就是索引）：

```c++
map<Key, T> myMap;
```

map中不会存在键相同的元素， multimap中允许多个元素拥有同一键。 multimap的使用方法与map的使用方法基本相同。

---



**map中的插入：**

```c++
map["yik"] = 2153000;
mp.insert(pair<string, int>("yik", 2153000));
```



**map中的查找：**

在利用下标访问map中的某个元素时，如果map中不存在相应键的元素，会自动在map中插入一个新元素，并将其值设置为默认值(对于整数，值为零；对于有默认构造函数的类型，会调用默认构造函数进行初始化)。

若下标访问操作过于频繁，容器中会出现大量无意义的元素，影响map的效率。因此一般情况下推荐使用find()函数来寻找特定键的元素。

```c++
mp.find(x)	//返回x的迭代器；否则返回end()。
```

==对map的迭代器解引用后，得到的是类型为pair<Key, T>的键值对。==

在C++11中，使用范围for循环会让代码简洁很多：

```c++
set<int> s;
for (auto x: s) cout << x << endl;
```



**自定义比较方式：**

维护一个存储整数，且较大值靠前的set：

```c++
struct cmp {
	bool operator()(int a, int b) { return a > b; }
};

set<int, cmp> s;
```



## STL算法：

---

![image-20230112115122597](C:\Users\yi'k\AppData\Roaming\Typora\typora-user-images\stl算法.png)

![image-20230112115221465](C:\Users\yi'k\AppData\Roaming\Typora\typora-user-images\stl算法2.png)

![image-20230112115313247](C:\Users\yi'k\AppData\Roaming\Typora\typora-user-images\stl算法3.png)

![image-20230112115414631](C:\Users\yi'k\AppData\Roaming\Typora\typora-user-images\stl算法4.png)



```c++
//使用next_permutation生成1到9的全排列。
int N = 9, a[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
do{
    for(int i = 0; i < N; i++) cout << a[i] <<" ";
    cout << endl;
}while(next_permutation(a, a + N));
```



```c++
//使用sort与unique查找数组a中第k小的值
int N = 10, a[] = {1, 3, 3, 7, 2, 5, 1, 2, 4, 6}, k = 3;
sort(a, a + N);
//unique将返回去重之后数组最后一个元素之后的地址，计算出的cnt为去重之后数组的长度
int cnt = unique(a, a + N) - a;
cout << a[k-1];
```



```c++
vector<int> v;
sort(range(v));
v.erase(unique(range(v)),v.end())	//元素去重
```



```c++
if(x^y)		//若x！=y
    
(a-b+mod*prime)%mod		//求a-b对mod取模，防止出现负数的做法
    
x^=1	//0变1，1变0
```


## 细节

```c++
//注意sqrt和sqrtl的使用场景
```

