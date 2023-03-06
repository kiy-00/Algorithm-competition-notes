## DP

---

### F. Zeros and Ones:

**题意：**


**思路：**
*	S的第i位等于popcount_parity(i)，即i的二进制表示中，非零位的个数的奇偶性。
*	假设i被包含在第k次构造中，i的最高位是2^k。
*	分m的奇偶性讨论，m为奇数时可以由偶数得出
*	



### E. Sending a Sequence Over the Network

**题意：**

将一个数列分成若干段，每一段的长度写在该段的前面或者后面，由此构成一个新的数列，现在给你一个数列，判断其是否是用这种方法构造出来的

**思路：**

dp，f[i]表示以第i个数结尾的序列是用上述方法构造出来的，最后答案在f[n]中。

**代码：**

```c++
void solve()
{
    int n;
    cin>>n;
    for (int i = 1; i <= n;i++)
        cin >> b[i], f[i] = 0;
 
    f[0] = 1;
 
    for (int i = 0; i <= n;i++){
        if(i-b[i]-1>=0&&f[i-b[i]-1])
            f[i] = 1;
        if(f[i]&&i+b[i+1]+1<=n)
            f[i + b[i+1] + 1] = 1;
    }
 
    if(f[n])
        cout << "YES\n";
    else
        cout << "NO\n";
 
    return;
}
```

