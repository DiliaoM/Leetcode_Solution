### #121 Best Time to Buy and Sell Stock

**Problems:**

Say you have an array for which the $i^{th}$ element is the price of a given stock on day $i$.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.



**My Answer:** （12%）

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        buy = 1
        mini = 0
        d = 0
        l = len(prices)
        while(buy < l):
            if prices[buy] < prices[mini]:
                mini = buy
            else:
                d = max(d,prices[buy]-prices[mini])
            buy += 1
        return d
```



**Other answer:**(79.95%)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        maxdiff = 0
        currentdiff = 0
        for buy in range(1,len(prices)):
            diff = prices[buy] - prices[buy-1]
            if currentdiff > 0:
                currentdiff += diff
            else:
                currentdiff = diff
            maxdiff = max(maxdiff,currentdiff)
        return maxdiff
```



Use their difference. It is very useful!.