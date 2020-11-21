## 题目
地上有一个 m 行 n 列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于 k 的格子。例如，当 k 为 18 时，机器人能够进入方格 [35, 37] ，因为 3+5+3+7=18。但它不能进入方格 [35, 38]，因为 3+5+3+8=19。请问该机器人能够到达多少个格子？

**示例 1**
```
输入：m = 2, n = 3, k = 1
输出：3
```

**示例 2**
```
输入：m = 3, n = 1, k = 0
输出：1
```

**提示**
* 1 <= n,m <= 100
* 0 <= k <= 20

## 代码
```JAVA
class Solution {
    private int m;
    private int n;
    private int k;
    private boolean[][] visited;

    public int movingCount(int m, int n, int k) {
        this.m = m;
        this.n = n;
        this.k = k;
        this.visited = new boolean[m][n];
        return movingCount(0, 0);
    }

    public int movingCount(int row, int col){
        int count = 0;
        if (row >= 0 && row < m && col >= 0 && col < n && getDigits(row, col) <= k && !visited[row][col]){
            visited[row][col] = true;
            count += 1 +  movingCount(row + 1, col) + movingCount(row, col + 1);
        }
        return count;
    }

    public int getDigits(int row, int col) {
        int result = 0;
        while(row != 0){
            result += row % 10;
            row /= 10;
        }
        while(col != 0){
            result += col % 10;
            col /= 10;
        }
        return result;
    }
}
```

## 思路

DFS + 剪枝即可。由于是递归，只需考虑向右向下移动的两个方向即可。时间空间复杂度均为 O(m * n)。