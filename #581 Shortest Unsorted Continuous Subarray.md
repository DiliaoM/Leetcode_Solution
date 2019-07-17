### #581 Shortest Unsorted Continuous Subarray



**Problems:**

Given an integer array, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the **shortest** such subarray and output its length.

**Example 1:**

```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```



**Approach 1: Using Sorting**

```c++
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        vector<int> verify;
        int begin=-1;
        int end = -2;
        for(int i=0;i<nums.size();i++)
            verify.push_back(nums[i]);
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size();i++)
        {
            if (verify[i] != nums[i])
            {
                if (begin==-1)
                    begin = i;
                end = i;
            }
        }
        return end-begin+1 ;
    }
};
```



#### Approach 4: Using Stack

**Algorithm**

The idea behind this approach is also based on selective sorting. We need to determine the correct position of the minimum and the maximum element in the unsorted subarray to determine the boundaries of the required unsorted subarray.

![Unsorted_subarray](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/Figures/581/Unsorted_subarray_2.PNG)

```c++
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        stack<int> mystack;
        int l = nums.size();
        int r = 0;
        for(int i=0;i<nums.size();i++)
        {
            while(!mystack.empty() && nums[mystack.top()] > nums[i])
            {
                l = min(mystack.top(),l);
                mystack.pop();
            }
            mystack.push(i);
        }
        while(!mystack.empty())
            mystack.pop();
        for(int i=nums.size()-1;i>=0;i--)
        {
            while(!mystack.empty() && nums[mystack.top()] < nums[i])
            {
                r = max(mystack.top(),r);
                mystack.pop();
            }
            mystack.push(i);
        }
        return r>l ? r-l+1 :0 ;
    }
};
```



