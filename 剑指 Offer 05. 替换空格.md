## 题目
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

**示例 1**
```
输入：s = "We are happy."
输出："We%20are%20happy."
```

**限制**
* 0 <= s 的长度 <= 10000

## 代码
```JAVA
class Solution {
    public String replaceSpace(String s) {
        char[] c = s.toCharArray();
        char[] padding = new char[]{'%','2','0'};
        int times = 0;
        for(int i = 0;i < c.length;i++){
            if (c[i] == ' '){
                times++;
            }
        }
        StringBuilder result = new StringBuilder(c.length + times * 2);
        for(int i = 0;i < c.length;i++){
            if (c[i] != ' '){
                result.append(c[i]);
            } else {
                result.append(padding);
            }
        }
        return result.toString();
    }
}
```

## 思路

由于字符串数组要变长，因而 0(N) 的空间复杂度没办法避免；由于需要扫描一遍字符串数组，因而 0(N) 的时间复杂度没办法避免。

接下来的取舍就是要不要扫两遍数组以减少多次数组扩容时内存拷贝的时间损耗了。这里选择了此方法。

* 时间复杂度：O(n)。
* 空间复杂度：O(n)。