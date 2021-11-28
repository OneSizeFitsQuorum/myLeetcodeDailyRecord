## 题目
打乱一个没有重复元素的数组。

**示例**
```
// 以数字集合 1, 2 和 3 初始化数组。
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// 打乱数组 [1,2,3] 并返回结果。任何 [1,2,3] 的排列返回的概率应该相同。
solution.shuffle();

// 重设数组到它的初始状态 [1,2,3]。
solution.reset();

// 随机返回数组 [1,2,3] 打乱后的结果。
solution.shuffle();
```

## 代码
```Java
class Solution {

    int[] origin;
    int length;
    Random r = new Random();

    public Solution(int[] nums) {
        origin = nums;
        length = nums.length;
    }
    
    public int[] reset() {
        return origin;
    }
    
    public int[] shuffle() {
        int[] result = origin.clone();
        for(int i = 0;i < length;i++){
            swap(result, i, r.nextInt(length - i) + i);
        }
        return result;
    }

    private void swap(int[] array,int left,int right){
        int tmp = array[left];
        array[left] = array[right];
        array[right] = tmp;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```

## 思路

著名的洗牌算法，建议背一下，一共有 n! 种可能。

* Fisher-Yates 洗牌算法跟暴力算法很像。在每次迭代中，生成一个范围在当前下标到数组末尾元素下标之间的随机整数。接下来，将当前元素和随机选出的下标所指的元素互相交换。
* 这一步模拟了每次从 “帽子” 里面摸一个元素的过程，其中选取下标范围的依据在于每个被摸出的元素都不可能再被摸出来了。此外还有一个需要注意的细节，当前元素是可以和它本身互相交换的，否则生成最后的排列组合的概率就不对了。
