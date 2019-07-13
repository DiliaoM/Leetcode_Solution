###  #66 Merge Sorted Array

**Problem:**

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**

- The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.
- You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*.



**Answer:**

Mine:

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int> nums3 ;
        int i=0;
        int j=0;
        if(nums2.size()==0 or n==0)
            nums3 = nums1;
        else if(nums1.size()==0 or m==0)
            nums3 = nums2;
        else
        {
            for(i;i<m;i++)
            {
                for(j;j<n;j++)
                {
                    if(nums1[i]<=nums2[j])
                    {
                        nums3.push_back(nums1[i]);
                        if(i!=m-1) 
                            break;
                        else
                        {
                            while(j<n)
                            {
                                nums3.push_back(nums2[j]);
                                j++;
                            }
                            break;
                        }
                    }
                    else
                    {
                        nums3.push_back(nums2[j]);
                        while(j==n-1 and i<m)
                        {
                            nums3.push_back(nums1[i]);
                            i++;
                        }
                    }
                        
                }
            }
        }
            
        nums1 = nums3;
    }
};
```



It is too complicated to understand. There is another solution to this problem.

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int len = m + n - 1;
        m--, n--;
        for (; m >= 0 || n >= 0;) {
            nums1[len--] = m < 0 ? nums2[n--] : n < 0 ? nums1[m--] : nums1[m] > nums2[n] ? nums1[m--] : nums2[n--];
        }
    }
};
```

The strategy is easier and simpler. We could think about the way that doing in an opposite direction.