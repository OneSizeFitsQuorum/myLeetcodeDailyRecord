## 题目
n 皇后问题 研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 n ，返回 n 皇后问题 不同的解决方案的数量。

**示例1**
![](static/51.jpg)
```
输入：n = 4
输出：2
解释：如上图所示，4 皇后问题存在两个不同的解法。
```

**示例2**
```
输入：n = 1
输出：1
```

**提示**
* 1 <= n <= 9
* 皇后彼此不能相互攻击，也就是说：任何两个皇后都不能处于同一条横行、纵行或斜线上。

## 代码
```JAVA
class Solution {
    
    public int num = 0;

    public int totalNQueens(int n) {
        char[][] chess = new char[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                chess[i][j] = '.';
        solve(chess, 0);
        return num;
    }

    private void solve(char[][] chess, int row) {
        if (row == chess.length) {
            num++;
            return;
        }
        for (int col = 0; col < chess.length; col++) {
            if (valid(chess, row, col)) {
                chess[row][col] = 'Q';
                solve(chess, row + 1);
                chess[row][col] = '.';
            }
        }
    }

    //row表示第几行，col表示第几列
    private boolean valid(char[][] chess, int row, int col) {
        //判断当前列有没有皇后,因为他是一行一行往下走的，
        //我们只需要检查走过的行数即可，通俗一点就是判断当前
        //坐标位置的上面有没有皇后
        for (int i = 0; i < row; i++) {
            if (chess[i][col] == 'Q') {
                return false;
            }
        }
        //判断当前坐标的右上角有没有皇后
        for (int i = row - 1, j = col + 1; i >= 0 && j < chess.length; i--, j++) {
            if (chess[i][j] == 'Q') {
                return false;
            }
        }
        //判断当前坐标的左上角有没有皇后
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (chess[i][j] == 'Q') {
                return false;
            }
        }
        return true;
    }
}
```
## 思路

经典回溯，比 51 题简单点，只用返回数量即可。应该是通过率最高的 hard 题目了，可以参照 51 题。