## 题目
实现 pow(x, n) ，即计算 x 的 n 次幂函数。

**示例 1**
```
输入：2.00000, 10
输出：1024.00000
```

**示例 2**
```
输入：2.10000, 3
输出：9.26100
```

**示例 3**
```
输入：2.00000, -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
```

**说明**
* -100.0 < x < 100.0
* 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

## 代码（暴力）
```JAVA
class Solution {
    public double myPow(double x, int n) {
        if (n < 0){
            return 1 / fastPow(x, 0L - n);
        }
        return fastPow(x, n);
    }

    public double fastPow(double x, long n){
        double res = 1;
        for(int i = 0;i < n;i++){
            res *= x; 
        }
        return res;
    }
}
```

## 代码（递归快速幂算法）
```Java
class Solution {
    public double myPow(double x, int n) {
        if (n < 0){
            return 1 / fastPow(x, 0L - n);
        }
        return fastPow(x, n);
    }

    public double fastPow(double x, long n){
        if(n == 0) {
            return 1;
        }
        double result = fastPow(x, n / 2);
        result *= result;
        if(n % 2 == 1){
            result *= x;
        }
        return result;
    }
}
```

## 代码（迭代快速幂算法）
```Java
class Solution {
    public double myPow(double x, int n) {
        if (n < 0){
            return 1 / fastPow(x, 0L - n);
        }
        return fastPow(x, n);
    }

    public double fastPow(double x, long n){
        double result = 1;
        double current = x;
        for(long i = n; i > 0; i >>= 1){
            if (i % 2 == 1){
                result *= current;
            }
            current *= current;
        }
        return result;
    }
}
```

## 思路

### 解法 1
这题最简单的就是暴力算法，将 x 连乘 n 次，如果 n < 0，我们可以用 1 / x，-n 来替换 x，n。另外我们需关注边界条件，尤其是正整数和负整数的不同范围限制，建议直接转换为 long。这种做法的时间复杂度是`O(n)`，肯定不是一个好做法。

### 解法 2
其实也可以用快速幂算法，假定我们已经得到了 x ^ (n / 2) 的结果，并且我们现在想得到 x ^ n 的结果。我们令 A 是 x ^ (n / 2) 的结果，我们可以根据 n 的奇偶性来分别讨论 x ^ n 的值。
* 如果 n 为偶数，我们可以用公式 (x ^ n) ^ 2 = x ^ (2 * n) 来得到 x ^ n = A * A 
* 如果 n 为奇数，那么 A * A = x ^ (n - 1)。直观上看，我们需要再乘一次 x ，即 x ^ n = A * A * x，即 n=A∗A∗x。该方法可以很方便的使用递归实现。我们称这种方法为 "快速幂"。
* 时间复杂度：`O(lgn)`
* 空间复杂度：`O(lgn)`

### 解法 3
![](static/50.png)
* 时间复杂度：`O(lgn)`
* 空间复杂度：`O(1)`