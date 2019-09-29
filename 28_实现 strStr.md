## 题目
实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

**示例1**
```
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例2**
```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

**说明**

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

## 代码
```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int len = needle.length();
        if (len < 1){
            return 0;
        }
        int index = -1;
        if((index = haystack.find(needle)) != string::npos){
            return index;
        }else{
            return -1;
        }
    }
};
```
## 思路

这题就是个字符串匹配的题，有很多字符串匹配算法，KMP，暴力等等都可以。这里偷个懒用`STL`里面的字符串匹配算法了。