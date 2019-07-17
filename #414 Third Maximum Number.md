### #414 Third Maximum Number



**Problem:**

Given a **non-empty** array of integers, return the **third** maximum number in this array. If it does not exist, return the maximum number. The time complexity must be in O(n).



**C++ Answer:** 

```c++
class Solution {
public:
    int thirdMax(vector<int>& nums) {
        set<int> newNums(nums.begin(), nums.end());
	    set<int>::iterator it = newNums.end();

        int len = newNums.size();
        if (len <= 2)
            return *prev(it, 1);
        else
            return *prev(it, 3);
    }
};
```

