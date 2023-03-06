##	C++中GCC编译器的内置函数

---

**__builtin_popcount(x)**

**__builtin_popcountll(x)**

用于计算整数类型数据中1的数量

```c++
n=13;	//二进制为1101
_builtin_popcount(n);	//结果是3
```

**__builtin_parity(x)**

**__builtin_parityll(x)**

用于检查数字的奇偶校验
返回二进制下1个数的奇偶性

```c++
n=13;
__builtin_parity(n);	//3个1，返回1
```

**__builtin_clz()**

**__builtin_clzll()  	**	对于long long类型

用于计算整数的前导零

```c++
n=13;
//0000 0000 0000 0000 0000 0000 0000 1101（32位整数）
__builtin_clz(n);	//前导零计数为28
```
**__builtin_ctz()**

**__builtin_ctzll()**

用于计算整数的尾随零

```c++
 int n = 12; //二进制是 1100
//0000 0000 0000 0000 0000 0000 0000 1100（32位整数）
__builtin_ctz(n);	//尾随零计数为2
```

