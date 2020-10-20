## 题目
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。（若队列中没有元素，deleteHead 操作返回 -1 )

**示例 1**
```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```

**示例 2**
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

**限制**
* 1 <= values <= 10000
* 最多会对 appendTail、deleteHead 进行 10000 次调用

## 代码
```JAVA
class CQueue {
    LinkedList<Integer> s1 = new LinkedList<>();
    LinkedList<Integer> s2 = new LinkedList<>();

    public CQueue() {}
    
    public void appendTail(int value) {
        s1.push(value);
    }
    
    public int deleteHead() {
        if (s2.size() == 0){
            while (s1.size() != 0){
                s2.push(s1.pop());
            }
        }
        if (s2.size() == 0){
            return -1;
        }
        return s2.pop();
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

## 思路

看代码就懂，关键在于如果模拟出队列先进先出的行为。需要注意的是 Java 的 Stack 是基于数组实现的，频繁增删性能较低，可以直接用链表模拟 Stack 即可，当然需要注意仅仅使用在尾部增删的 API 来保证题意。

* 空间复杂度：O(n)
* 时间复杂度：每个元素均只会出入栈一次，均摊后依然为 O(1)