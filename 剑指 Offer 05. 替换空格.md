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
        int numOfBlanks = 0;
        for(int i = 0;i < s.length();i++){
            if (s.charAt(i) == ' '){
                numOfBlanks++;
            }
        }
        StringBuilder res = new StringBuilder(s.length() + numOfBlanks * 2);
        for(int i = 0;i < s.length();i++){
            char c = s.charAt(i);
            if (c == ' '){
                res.append("%20");
            } else {
                res.append(c);
            }
        }
        return res.toString();
    }
}
```

## 思路

由于字符串数组要变长，因而 0(N) 的空间复杂度没办法避免；由于需要扫描一遍字符串数组，因而 0(N) 的时间复杂度没办法避免。

接下来的取舍就是要不要扫两遍数组以减少多次数组扩容时内存拷贝的时间损耗了。这里选择了此方法。

* 时间复杂度：O(n)。
* 空间复杂度：O(n)。