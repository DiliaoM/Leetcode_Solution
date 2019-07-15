### #169 Majority Element



#### **Problem:**

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.



#### **Approach 1 : Brute Force**

**Complexity Analysis:**

- Time complexity : $O(n^2)$

  The brute force algorithm contains two nested `for` loops that each run for $n$ iterations, adding up to quadratic time complexity.

- Space complexity: $O(1)$

  ​



#### Approach 2 : HashMap

We could use a `Hashmap` that maps elements to counts in order to count occurrences in linear time by looping over `nums`. Then, we simply return the key with maximum value.

```python
class Solution:
    def majorityElement(self, nums):
        counts = collections.Counter(nums)
        return max(counts.keys(), key=counts.get)
```

**Complexity Analysis:**

- Time complexity : $O(n)$

- Space complexity: $O(n)$

  At most, the `Hashmap` can contain $n-\frac{n}{2}$ associations, so it occupies $O(n)$ space. This is because an arbitrary array of length $n$ can contain $n$ distinct values, but `nums` is guaranteed to contain a majority element, which will occupy (at minimum) $\frac{n}{2} + 1$ array indices. 


> Python-collections
>
> 1. `OrderedDict` is a `dict` in order. It has functions such as pop, clear, move_to_end, del and so on.
> 2. `deque` is two-way linked-list. 
> 3. `Counter` is subclass of `dict`. And some usage is the same as `dict`. Besides, it has two more functions: `most_common()`, `elements()`. 




#### Approach 3 : Sorting

If the elements are sorted in monotonically increasing(or decreasing) order, the majority element can be found at index $\frac{n}{2}$ .

![Sorting middle index overlap](https://leetcode.com/articles/Figures/169/sorting.png)

```python
# By Python
class Solution:
    def majorityElement(self, nums):
        nums.sort()
        return nums[len(nums)//2]
```

```c++
//By C++.
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        return nums[nums.size()/2];
    }
};
```

**Complexity Analysis:**

- Time complexity : $O(nlgn)$

  Sorting the array costs $O(nlgn)$  time in Python and Java, so it dominates the overall runtime.

- Space complexity: $O(1)$ or  $O(n)$ 

  We sorted `nums` in place here - if that is not allowed, then we must spend linear additional space on a copy of `nums` and sort the copy instead.

  ​

#### Approach 4 : Randomization

```python
import random

class Solution:
    def majorityElement(self, nums):
        majority_count = len(nums)//2
        while True:
            candidate = random.choice(nums)
            if sum(1 for elem in nums if elem == candidate) > majority_count:
                return candidate
```

**Complexity Analysis:**

- Time complexity : $O(\infty)$

- Space complexity: $O(1)$ 

  ​

#### Approach 5 : Divide and Conquer

If we know the majority element in the left and right halves of an array, we can determine which is the global majority element in linear time.

**Algorithm**

Here, we apply a classical divide & conquer approach that recurses on the left and right halves of an array until an answer can be trivially achieved for a length-1 array. Note that because actually passing copies of subarrays costs time and space, we instead pass `lo`and `hi` indices that describe the relevant slice of the overall array. In this case, the majority element for a length-1 slice is trivially its only element, so the recursion stops there. If the current slice is longer than length-1, we must combine the answers for the slice's left and right halves. If they agree on the majority element, then the majority element for the overall slice is obviously the same. If they disagree, only one of them can be "right", so we need to count the occurrences of the left and right majority elements to determine which subslice's answer is globally correct. The overall answer for the array is thus the majority element between indices 0 and nn.

```python
class Solution:
    def majorityElement(self, nums, lo=0, hi=None):
        def majority_element_rec(lo, hi):
            # base case; the only element in an array of size 1 is the majority
            # element.
            if lo == hi:
                return nums[lo]

            # recurse on left and right halves of this slice.
            mid = (hi-lo)//2 + lo
            left = majority_element_rec(lo, mid)
            right = majority_element_rec(mid+1, hi)

            # if the two halves agree on the majority element, return it.
            if left == right:
                return left

            # otherwise, count each element and return the "winner".
            left_count = sum(1 for i in range(lo, hi+1) if nums[i] == left)
            right_count = sum(1 for i in range(lo, hi+1) if nums[i] == right)

            return left if left_count > right_count else right

        return majority_element_rec(0, len(nums)-1)

```

**Complexity Analysis:**

- Time complexity : $O(nlgn )$
- Space complexity: $O(lgn )$ 

