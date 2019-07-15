### #122 Best Time to Buy and Sell Stock II



**Problem:**

Say you have an array for which the $i^{th}$ element is the price of a given stock on day $i$.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).





**Approach : Peak Valley Approach**

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        maxprofit = 0
        l = len(prices)
        i = 1
        while(i<l):
            while(i<l and prices[i]-prices[i-1]<=0):
                i += 1
            valley = prices[i-1]
            while(i<l and prices[i]-prices[i-1]>=0):
                i += 1
            peak = prices[i-1]
            maxprofit += peak-valley
        return maxprofit
```



##### Approach : Simple One Pass

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxprofit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1])
                maxprofit += prices[i] - prices[i - 1];
        }
        return maxprofit;
    }
}
```

