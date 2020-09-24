## 题目
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

**示例 1**
现有矩阵 matrix 如下：
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
给定 target = 5，返回 true。

给定 target = 20，返回 false。

**限制**
* 0 <= n <= 1000
* 0 <= m <= 1000

## 代码
```JAVA
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        int rowLength = matrix.length;
        if (rowLength <= 0) return false;
        int colLength = matrix[0].length;
        if (colLength <= 0) return false;
        int rowIndex = 0;
        int colIndex = colLength - 1;
        while(rowIndex < rowLength && colIndex >= 0){
            if (matrix[rowIndex][colIndex] == target){
                return true;
            } else if (matrix[rowIndex][colIndex] > target){
                colIndex--;
            } else {
                rowIndex++;
            }
        }
        return false;
    }
}
```

## 思路

从右上角开始判断，保证每次结果指示的单向性即可。

* 时间复杂度：O(n + m)。
* 空间复杂度：O(1)。