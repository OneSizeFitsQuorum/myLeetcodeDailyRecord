## 题目
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 重复 元素值的数组 numbers ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一次旋转，该数组的最小值为1。  

**示例 1**
```
输入：[3,4,5,1,2]
输出：1
```

**示例 2**
```
输入：[2,2,2,0,1]
输出：0
```

## 代码(二分法)
```JAVA
class Solution {
    public int minArray(int[] numbers) {
        int left = 0;
        int right = numbers.length - 1;
        while(left < right){
            int mid = left + (right - left) / 2;
            if (numbers[mid] < numbers[right]){
                right = mid;
            } else if (numbers[mid] > numbers[right]) {
                left = mid + 1;
            } else {
                right--;
            }
        }
        return numbers[left];
    }
}
```

## 代码(分治法)
```JAVA
class Solution {
    public int minArray(int[] numbers) {
        return minArray(numbers, 0, numbers.length - 1);
    }

    public int minArray(int[] numbers, int left, int right) {
        if (left + 1>= right){
            return Math.min(numbers[left], numbers[right]);
        }
        if(numbers[left] < numbers[right]){
            return numbers[left];
        }
        int mid = left + (right - left) / 2;
        return Math.min(minArray(numbers, left, mid - 1), minArray(numbers, mid, right)); 
    }
}
```

## 思路

### 解法 1

* 旋转排序数组 nums 可以被拆分为 2 个排序数组 nums1，nums2，并且 nums1 任一元素 >= nums2 任一元素；因此，考虑二分法寻找此两数组的分界点 nums[i] （即第 2 个数组的首个元素）。
* 设置 left, right 指针在 nums 数组两端，mid 为每次二分的中点：
    * 当 nums[mid] > nums[right] 时，mid 一定在第 1 个排序数组中，i 一定满足 mid < i <= right，因此执行 left = mid + 1；
    * 当 nums[mid] < nums[right] 时，mid 一定在第 2 个排序数组中，i 一定满足 left < i <= mid，因此执行 right = mid；
    * 当 nums[mid] == nums[right] 时，是此题对比 153 题 的难点（原因是此题中数组的元素可重复，难以判断分界点 ii 指针区间）；
        * 例如 [1, 0, 1, 1, 1] 和 [1, 1, 1, 0, 1] ，在 left = 0, right = 4, mid = 2 时，无法判断 mid 在哪个排序数组中。
        * 我们采用 right = right - 1 解决此问题，证明：
            1. 此操作不会使数组越界：因为迭代条件保证了 right > left >= 0；
            2. 此操作不会使最小值丢失：假设 nums[right] 是最小值，有两种情况：
                * 若 nums[right] 是唯一最小值：那就不可能满足判断条件 nums[mid] == nums[right]，因为 mid < right（left != right 且 mid = (left + right) / 2 向下取整）；
                * 若 nums[right] 不是唯一最小值，由于 mid < right 而 nums[mid] == nums[right]，即还有最小值存在于 [left, right - 1] 区间，因此不会丢失最小值。
* 时间复杂度 `O(logN)`，在特例情况下会退化到 `O(N)`（例如 [1, 1, 1, 1]）。

### 解法 2

可以使用分治法，递归分开判断寻找最小值，时间复杂度为`O(lgn)`，代码相比 153 题都不用改。
