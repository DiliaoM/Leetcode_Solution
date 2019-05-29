## #27 Remove Element

> \#26 Remove Duplicates from Sorted Array 与此解法相似。

**Problem:** 

​	Given an array *nums* and a value *val*, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.





我的c++解法：

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        if(nums.empty())
            return 0;
        int i=0,k=0;
        while(i < nums.size())
        {
            if(nums[i++] != val)
                nums[k++] = nums[i-1]; //注意k++和++k的区别。
        }
        return k;
    }
};
```



100%排位的c++解法：

```c++
class Solution {
public:
	int removeElement(vector& nums, int val) {
		for(int i =0; i<nums.size(); i++) {
			if(nums[i] == val) {
				nums.erase(nums.begin()+i);
				i--;
			}
		}
		return nums.size();
	}
};
```

