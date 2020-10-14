## 题目
输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

**示例 1**
```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**示例 2**
```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

**限制**
* 0 <= 节点个数 <= 5000

## 代码
```JAVA
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    private Map<Integer,Integer> valueToIndex = new HashMap<>();
    private int index;
    private int[] preorder;

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0 || inorder.length == 0){
            return null;
        }
        this.preorder = preorder;
        this.index = 0;
        for(int i = 0;i < inorder.length;i++){
            valueToIndex.put(inorder[i],i);
        }
        return helper(0, preorder.length - 1);
    }

    public TreeNode helper(int left, int right){
        if (right < left){
            return null;
        }
        int val = preorder[index++];
        TreeNode root = new TreeNode(val);
        int index = valueToIndex.get(val);

        root.left = helper(left, index - 1);
        root.right = helper(index + 1, right);

        return root;
    }
}
```

## 思路

* 创建哈希表存储中序序列：value -> its index。
* 方法 helper 的参数是中序序列中当前子树的左右边界，该方法仅用于检查子树是否为空。下面分析 helper(left = 0, right = n - 1) 的逻辑：
* 如果 in_right < in_left，说明子树为空，返回 None。
* 选择先序遍历的第一个节点作为根节点。
* 假设根节点在中序遍历中索引为 index。从 left 到 index - 1 属于左子树，从 index + 1 到 right 属于右子树。
* 根据先序遍历逻辑，递归创建左子树 helper(left, index - 1) 和右子树 helper(index + 1, right)。（注意一定得先左子树再右子树。)
* 返回根节点 root。

![](static/105.png)