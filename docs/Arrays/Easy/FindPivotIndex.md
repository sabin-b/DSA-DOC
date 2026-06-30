# Find Pivot Index

[Problem Link](https://leetcode.com/problems/find-pivot-index/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an array of integers `nums`, compute the pivot index of this array.

The pivot index is the index where the sum of all numbers to the left is equal to the sum of all numbers to the right. If no such index exists, return `-1`.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [1, 7, 3, 6, 5, 6]
    Output: 3
    Explanation: The pivot index is 3. Left sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11. Right sum = nums[4] + nums[5] = 5 + 6 = 11.

    **Example 2:**
    Input: nums = [1, 2, 3]
    Output: -1
    Explanation: No index satisfies the condition.

    **Example 3:**
    Input: nums = [2, 1, -1]
    Output: 0
    Explanation: The pivot index is 0. Left sum = 0 (no elements to left). Right sum = nums[1] + nums[2] = 1 + -1 = 0.

### Approach: Prefix Sum

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

We first compute the total sum of the array. Then we iterate through the array, maintaining a running left sum. At each index, we subtract the current element from the right sum (initially total sum) and check if the left and right sums are equal.

```typescript
function pivotIndex(nums: number[]): number {
  let rightSum = 0;
  let leftSum = 0;
  for (let i = 0; i < nums.length; i++) rightSum += nums[i];
  for (let i = 0; i < nums.length; i++) {
    rightSum -= nums[i];
    if (rightSum === leftSum) return i;
    leftSum += nums[i];
  }
  return -1;
}

console.log(pivotIndex([1, 7, 3, 6, 5, 6])); // 3
console.log(pivotIndex([1, 2, 3]));           // -1
console.log(pivotIndex([2, 1, -1]));          // 0
```
