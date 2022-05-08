###



### 代码：

```java
class Solution {
    public int maxProfit(int[] nums) {
        if(nums.length < 2){
            return 0;
        }
        int maxRes = 0;
        int minVal = nums[0];
        for(int i = 0; i < nums.length; i++){
            minVal = Math.min(minVal,nums[i]);
            maxRes = Math.max(nums[i] - minVal, maxRes);
        }
        return maxRes;
    }
}
```

