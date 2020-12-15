## 题目
给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n 都是整数，n>1 并且 m>1），每段绳子的长度记为 k[0],k[1]...k[m - 1] 。请问 k[0]*k[1]*...*k[m - 1] 可能的最大乘积是多少？例如，当绳子的长度是 8 时，我们把它剪成长度分别为 2、3、3 的三段，此时得到的最大乘积是 18。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

**示例 1**
```
输入：2
输出：1
解释：2 = 1 + 1, 1 × 1 = 1
```

**示例 2**
```
输入：10
输出：36
解释：10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

**提示**
* 2 <= n <= 1000

## 代码
```JAVA
class Solution {
    public int cuttingRope(int n) {
        if (n <= 3){
            return n - 1;
        }
        switch (n % 3) {
            case 0:
                return (int)fastThreePow(n / 3);
            case 1:
                return (int)(fastThreePow(n / 3 - 1) * 4 % 1000000007);
            case 2:
                return (int)(fastThreePow(n / 3) * 2 % 1000000007);
        }
        return 0;
    }

    public long fastThreePow(int n){
        long result = 1;
        long current = 3;
        for(int i = n;i > 0; i >>= 1){
            if (i % 2 == 1) {
                result = (result * current) % 1000000007; 
            }
            current = (current * current) % 1000000007;
        }
        return result;
    }
}
```

## 思路

贪心算法。原理推算可以参考此 [博客](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/solution/mian-shi-ti-14-ii-jian-sheng-zi-iitan-xin-er-fen-f/)。主要需要解决整数溢出问题。

* 时间复杂度 ：O(lgN)
* 空间复杂度 ：O(1)