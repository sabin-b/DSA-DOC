# Two Sum

[Problem Link](https://leetcode.com/problems/two-sum/){:target="_blank" rel="noopener noreferrer"}

> **Pattern:** Hash Map | **Retrack Date:** 13/07/2026

### Description

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input has exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [2, 7, 11, 15], target = 9
    Output: [0, 1]
    Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

    **Example 2:**
    Input: nums = [3, 2, 4], target = 6
    Output: [1, 2]

    **Example 3:**
    Input: nums = [3, 3], target = 6
    Output: [0, 1]

### Approach: One-Pass Hash Map

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

We iterate through the array once. For each element, compute its complement (`target - nums[i]`). If the complement exists in the map, we've found the pair and return both indices. Otherwise, store the current number and its index in the map.

```typescript
function twoSum(nums: number[], target: number): number[] {
  if (!Array.isArray(nums) || nums.length === 0) return nums;

  const map = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) return [map.get(complement), i];
    map.set(nums[i], i);
  }
  return [];
}

console.log(twoSum([2, 7, 11, 15], 9)); // [0, 1]
console.log(twoSum([3, 2, 4], 6));      // [1, 2]
console.log(twoSum([3, 3], 6));         // [0, 1]
```

### Explanation

- Use a `Map` to store each number and its index as we iterate
- For each number, calculate the complement (`target - nums[i]`)
- If complement is in the Map, return `[map.get(complement), i]`
- Otherwise, store `nums[i]` with index `i` and continue
- Time: O(n) single pass | Space: O(n) for the Map

| Approach | Time | Space |
|----------|------|-------|
| One-Pass Hash Map | O(n) | O(n) |
