## #35 Search Insert Position

**Problem:**

​	Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.



c++解法：

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int i=0;
        for(i;i<nums.size();i++) //for语句会比while语句快，因为while语句总要计算nums.size() （我猜）
        {
            if(nums[i] >= target)
                return i;
        }
        return i;
    }
};
```

