# #1 Two Sum 

使用查找表来解决该问题。

设置一个map容器mapp用来记录元素的索引和值，然后遍历nums。



STL中，**map**对应的数据结构是**红黑树**，红黑树是一种近似于平衡的二叉查找树。里面的数据是有序的，在红黑树上做查找操作的时间复杂度为**O(logN)**。

**unordered_map**对应**哈希表**，哈希表的特点是查找效率高，时间复杂度为常数级别**O(1)**，而额外空间复杂度则要高出许多。

常用函数：

- bucket函数：定位元素所在的桶。返回key值为输入参数k的元素的所在桶号。
- count函数：搜索容器中key值作为输入参数k的元素，并返回找到元素的数量。
- clear操作：清除map中所有元素。
- erase操作：删除map中指定位置的元素。
- insert操作：在map指定位置添加pair类型的元素。
- find操作：获取map中元素的迭代器。
- begin，end：map的正向迭代器的起始位置与终点位置。





**实现代码：**

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> mapp;
        vector<int> result;
        for(int i=0;i<nums.size();i++){
            mapp[nums[i]] = i;
        }
        for(int i=0;i<nums.size();i++){
            int j = target - nums[i];
            if (mapp.count(j) && mapp[j]!=i){ //count 是搜索容器中key值为输入参数k的元素
                result.push_back(i);
                result.push_back(mapp[j]);
                break;
            }
        }
        return result;
    }
};
```

