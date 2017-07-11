---
title: PalindromeNumber
date: 2017-07-11 22:12:12
tags: leetcode
---

题目：Determine whether an integer is a palindrome. Do this without extra space.

思路：不能转成字符串来处理，因为不允许额外空间。直接将原数取反后，和原数进行比较。

特殊情况：

- 负数不是回文数字，因此直接判定FALSE。
- 只要是回文数字，就不会出现溢出。若溢出，则一定不是回文数字。

代码：

```c
bool isPalindrome(int x) {
	if (x < 0) return false;
    int t = x, y = 0;
    while (t > 0){
                y = y * 10 + t % 10;
                t = t / 10;
        }
    return x == y;
}
```

提交虽然通过了，但看网上一些大牛的答案，考虑了计算过程中不溢出的要求。例如，上面代码中，当`y * 10 > 2^31 - 1`就会发生溢出，截断高位后加上`t % 10`，就可能和原来的数相等。因此另一种保证不溢出的思路是，**每次取最高和最低位比较，然后掐头去尾后重复进行。**

以数字95349为例：

```
95349 % 10 => 9
95349 / 10000 => 95349 / 10^4 => 9
```

可以看出我们可以通过模10来取其最低位，除`10^(n-1)`来取其最高位，将其最高位和最低位进行比较，便可以得出当前是否符合回文要求了。

比较完最高位和最低位后，如何除掉这两位呢？

```
95349 % 1000 => 95349 % 10^4 = 5349
95349 / 10 = 9534
```

如此一来，便完成了掐头去尾了。

代码：

```c
int a = x, h = 1;
    if (a < 0) return false;
    while (a / h >= 10) {
        h = h * 10;
    }
    while (a > 0) {
        if (a / h != a % 10) return false;
        a = a % h;
        a = a / 10;
        h = h / 100;
    }
    return true;
```

参考：https://segmentfault.com/a/1190000000453441