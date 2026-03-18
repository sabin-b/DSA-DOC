# Best Time to Buy and Sell Stock

[Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

### Description

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`th day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

!!! example "Test Cases"

    **Example 1:**
    Input: prices = [7,1,5,3,6,4]
    Output: 5
    Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
    Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

    **Example 2:**
    Input: prices = [7,6,4,3,1]
    Output: 0
    Explanation: In this case, no transaction is done, and the max profit is 0.

### Approach 1: One Pass

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This efficient approach involves iterating through the `prices` array just once. We maintain two key variables:
- `minValue`: Keeps track of the lowest stock price found so far.
- `maxProfit`: Stores the maximum profit we could have achieved.

For each day, we first update `minValue` if the current day's price is a new low. Then, we calculate the potential profit if we were to sell on the current day (which is `prices[i] - minValue`) and update `maxProfit` if this potential profit is higher than any we've seen before.

```typescript
function maxProfit(prices: number[]): number {
  let maxProfit = 0;
  let minValue = prices[0];
  
  for (let i = 1; i < prices.length; i++) {
    // Find the minimum buy price so far
    minValue = Math.min(prices[i], minValue);
    
    // Check if selling today would yield a new max profit
    maxProfit = Math.max(prices[i] - minValue, maxProfit);
  }
  
  return maxProfit;
}

console.log(maxProfit([7, 1, 5, 3, 6, 4])); // 5
console.log(maxProfit([7, 6, 4, 3, 1])); // 0
```
