code:  
Python:  
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        max_profit = 0
        cost = 10**4
        for i in range(len(prices)):
            if prices[i] < cost:
                cost = prices[i]
            elif prices[i] - cost > max_profit:
                max_profit = prices[i] - cost
        
        return max_profit
```        
