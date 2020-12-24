**买卖股票的最佳时机II**

**题目：**

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。



**解法一： 贪心，这道题用这个有点违规，因为贪心算法要求能够当天把股票卖掉， 然后在当天再把股票买回来**

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        if (prices.length < 2) {
            return profit;
        }

        for (int i = 1, j = 0; i < prices.length; i++, j++) {
            //如果第二天股票的价格比前一天高就卖出
            profit += prices[j] < prices[i] ? prices[i] - prices[j] : 0;
        }
        return profit;
    }
}
```

时间复杂度：O(n)

空间复杂度：O(1)


**解法二：迭代**

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        int i = 0;
        while (i < prices.length) {
            //找出当前这一区间中最低的价格
            while (i < prices.length - 1 && prices[i] >= prices[i + 1])
                i++;
            int minPrice = prices[i++];

            //找出当前这一区间最大的价格
            while (i < prices.length - 1 && prices[i] <= prices[i + 1])
                i++;

            //最终利润加上最大价格-最低价格
            profit += i < prices.length ? prices[i++] - minPrice : 0;
        }
        return profit;
    }
}
```

时间复杂度：O(n)

空间复杂度：O(1)