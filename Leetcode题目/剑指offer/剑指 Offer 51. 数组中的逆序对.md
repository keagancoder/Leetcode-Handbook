### 题目描述

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

**示例 1:**

```java
输入: [7,5,6,4]
输出: 5
```

---

### 解题思路：

#### 归并算法：

归并算法划分两个步骤，分别是划分和合并两个过程；逆序数对就可以通过合并过程来计算。

##### 代码：

```java
class Solution {
    private int[] temp;
    public int reversePairs(int[] nums) {
        int n = nums.length;
        temp = new int[n];
        return mergeSort(nums,0,n-1);
    }
    public int mergeSort(int[] nums, int l, int r){
        if(l >= r) return 0;
        int m = l + (r - l)/2;
        int res = mergeSort(nums,l,m)+mergeSort(nums,m+1,r);
        //合并
        int i = l, j = m+1;
        int idx = 0;
        while(i <= m && j <= r){
            if(nums[i] <= nums[j]){
                temp[idx++] = nums[i++];
            }else{
                res += m - i + 1;
                temp[idx++] = nums[j++];
            }
        }
        while(i <= m){
            temp[idx++] = nums[i++];
        }
        while(j <= r){
            temp[idx++] = nums[j++];
        }
        for(int k = l; k <= r; k++){
            nums[k] = temp[k-l];
        }
        return res;
    }
}
```



