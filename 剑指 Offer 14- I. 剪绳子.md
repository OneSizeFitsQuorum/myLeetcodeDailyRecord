## 题目
给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n 都是整数，n>1 并且 m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是 8 时，我们把它剪成长度分别为 2、3、3 的三段，此时得到的最大乘积是 18。

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
* 2 <= n <= 58

## 代码（动规）
```JAVA
class Solution {
    public int cuttingRope(int n) {
        if (n <= 1){
            return 0;
        } else if (n <= 3){
            return n - 1;
        }
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        for(int i = 4;i <= n;i++){
            int max = Integer.MIN_VALUE;
            for(int j = 0;j <= i / 2;j++){
                max = Math.max(max, dp[j] * dp[i - j]);
            }
            dp[i] = max;
        }
        return dp[n];
    }
}
```

## 代码（贪心）
```JAVA
class Solution {
    public int cuttingRope(int n) {
        if (n <= 1){
            return 0;
        } else if (n <= 3){
            return n - 1;
        }
        switch (n % 3) {
            case 0:
                return (int)Math.pow(3, n / 3);
            case 1:
                return (int)Math.pow(3, n / 3 - 1) * 4;
            case 2:
                return (int)Math.pow(3, n / 3) * 2;
        }
        return 0;
    }
}
```

## 思路

### 解法 1

动规算法。
* 时间复杂度：O(N^2)
* 空间复杂度：O(N)

### 解法 2

贪心算法。原理推算可以参考此[博客](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/solution/mian-shi-ti-14-i-jian-sheng-zi-tan-xin-si-xiang-by/)。
* 时间复杂度 ：O(1)
* 空间复杂度 ：O(1)