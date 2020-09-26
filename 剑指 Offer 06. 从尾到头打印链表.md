## 题目
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例 1**
```
输入：head = [1,3,2]
输出：[2,3,1]
```

**限制**
* 0 <= 链表长度 <= 10000

## 代码
```JAVA
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
        int count  = 0;
        ListNode cur = head;
        while(cur != null){
            count++;
            cur = cur.next;
        }
        int[] result = new int[count];
        cur = head;
        while(cur != null){
            result[--count] = cur.val;
            cur = cur.next;
        }
        return result;
    }
}
```

## 思路

两次遍历链表即可，先计数再存数，这样可以避免 int 的拆装箱。

* 时间复杂度：O(n)。
* 空间复杂度：O(1)。