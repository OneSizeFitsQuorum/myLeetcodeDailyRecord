## 题目
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

**示例 1**
```
输入：n = 1
输出：[1,2,3,4,5,6,7,8,9]
```

**说明**
* 用返回一个整数列表来代替打印
* n 为正整数

## 代码（大数）
```JAVA
class Solution {
    public int[] printNumbers(int n) {
        BigNumer num = new BigNumer(n);
        num.compute();
        return num.getResult();
    }
}

class BigNumer {
    private char[] value;
    private int[] result;

    public BigNumer(int n) {
        value = new char[n];
        for(int i = 0;i < n;i++){
            value[i] = '0';
        }
        result = new int[(int)Math.pow(10, n) - 1];
    }

    public void compute(){
        for(int i = 0;i < result.length;i++){
            int carry = 1;
            for(int j = value.length - 1;j >= 0;j--){
                char sum = (char)(value[j] + carry);
                if (sum > '9') {
                    value[j] = '0';
                } else {
                    value[j] = sum;
                    break;
                }
            }
            for(int j = 0;j < value.length;j++){
                if(value[j] != '0') {
                    result[i] = Integer.valueOf(new String(value).substring(j));
                    break;
                }
            }
        }
    }

    public int[] getResult() {
        return result;
    }
}
```

## 代码（递归）
```Java
class Solution {

    private char[] values;
    private int[] res;
    private int cursor;

    public int[] printNumbers(int n) {
        res = new int[(int)Math.pow(10, n) - 1];
        for(int digit = 1;digit <= n;digit++){
            values = new char[digit];
            for(char i = '1';i <= '9';i++){
                values[0] = i;
                dfs(digit, 1);
            }
        }
        return res;
    }

    public void dfs(int digit, int index){
        if (digit == index) {
            res[cursor++] = Integer.valueOf(new String(values));
            return;
        }
        for(char i = '0';i <= '9';i++){
            values[index] = i;
            dfs(digit,index + 1);
        }
    }
}
```

## 思路

### 解法 1
大数加法。

* 时间复杂度 O(10^n) ： 生成长度为 10^n 的列表需使用 O(10^n) 时间。
* 空间复杂度 O(1) ： 建立列表需使用 O(1) 大小的额外空间（ 列表作为返回结果，不计入额外空间 ）。

### 解法 2

递归。

* 时间复杂度 O(10^n) ： 递归的生成的排列的数量为 10^n。
* 空间复杂度 O(1) ： 建立列表需使用 O(1) 大小的额外空间（ 列表作为返回结果，不计入额外空间 ）。
