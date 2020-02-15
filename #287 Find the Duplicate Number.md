# #287 Find the Duplicate Number



**Problem:**

Given an array *nums* containing *n* + 1 integers where each integer is between 1 and *n* (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Example 1:**

```
Input: [1,3,4,2,2]
Output: 2
```

**Example 2:**

```
Input: [3,1,3,4,2]
Output: 3
```

**Note:**

1. You **must not** modify the array (assume the array is read only).
2. You must use only constant, *O*(1) extra space.
3. Your runtime complexity should be less than *O*(*n*2).
4. There is only one duplicate number in the array, but it could be repeated more than once.



**Solution:**

1. Binary Search

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        low = 1
        high = len(nums)-1
        while low < high :
            mid = (high+low)//2 # 除法向下取整
            c = sum(n<=mid for n in nums)
            if c <= mid :
                low = mid+1
            else:
                high = mid
        return low
```

2. Cycle Detection

   First off, we can easily show that the constraints of the problem imply that a cycle *must* exist. Because each number in `nums` is between `1` and `n`, it will necessarily point to an index that exists. Therefore, the list can be traversed infinitely, which implies that there is a cycle. Additionally, because `0` cannot appear as a value in `nums`, `nums[0]` cannot be part of the cycle. Therefore, traversing the array in this manner from `nums[0]` is equivalent to traversing a cyclic linked list.
   
   
   
   ```c++
   class Solution {
   public:
       int findDuplicate(vector<int>& nums) {
           int slow = nums[0];
           int fast = nums[nums[0]];
           
           while(fast != slow)
           {
               fast = nums[nums[fast]];
               slow = nums[slow];
           }
           
           int mid = 0;
           while(mid != slow)
           {
               mid = nums[mid];
               slow = nums[slow];
           }
           return mid;
       }
   };
   ```
   