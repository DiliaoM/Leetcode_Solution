#458 Poor Pigs

**Probrem:**

There are 1000 buckets, one and only one of them is poisonous, while the rest are filled with water. They all look identical. If a pig drinks the poison it will die within 15 minutes. What is the minimum amount of pigs you need to figure out which bucket is poisonous within one hour?

Answer this question, and write an algorithm for the general case.

**General case:** 

If there are `n` buckets and a pig drinking poison will die within `m` minutes, how many pigs (`x`) you need to figure out the **poisonous** bucket within `p` minutes? There is exactly one bucket with poison.

 

**Note:**

1. A pig can be allowed to drink simultaneously on as many buckets as one would like, and the feeding takes no time.
2. After a pig has instantly finished drinking buckets, there has to be a **cool down time** of *m* minutes. During this time, only observation is allowed and no feedings at all.
3. Any given bucket can be sampled an infinite number of times (by an unlimited number of pigs).



Idea:

可以考虑最基础的情况。按照题目的要求，一只猪可有（`p/m+1`）种状态。（多个平面的思考）。

以题目为例，如果有5桶，那么一只猪就可以判断出来：15mins ，30mins，45mins，60mins die and alive. 

那么如果是25桶，可以想成一个5*5的矩阵。一只猪测试每行的混合物，一只猪测每列的混合物。如果哪个时间段死了就是相应的行和列。

以此类推，就发现是幂数的关系。



Cpp:

```c++
class Solution {
public:
    int poorPigs(int buckets, int minutesToDie, int minutesToTest) {
        if (buckets == 1)
            return 0;
        int m = minutesToTest/minutesToDie + 1;
        int n = 0;
        int newbuckets = 1;
        while (buckets > newbuckets)
        {   
            n++;
            newbuckets *= m;
        }
        return n;
    }
};
```

