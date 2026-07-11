# Find Pivot Index

[Problem Link](https://leetcode.com/problems/find-pivot-index/){:target="_blank" rel="noopener noreferrer"}

> **Pattern:** Prefix Sum | **Retrack Date:** 14/07/2026

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

### Approach 1: Brute Force

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

For each index, calculate the sum of all elements to the left and all elements to the right, then compare.

```typescript
function pivotIndex(nums: number[]): number {
  for (let i = 0; i < nums.length; i++) {
    let leftSum = 0;
    let rightSum = 0;

    for (let l = 0; l < i; l++) {
      leftSum += nums[l];
    }

    for (let r = i + 1; r < nums.length; r++) {
      rightSum += nums[r];
    }

    if (leftSum === rightSum) return i;
  }

  return -1;
}

console.log(pivotIndex([1, 7, 3, 6, 5, 6])); // 3
console.log(pivotIndex([1, 2, 3]));           // -1
console.log(pivotIndex([2, 1, -1]));          // 0
```

### Approach 2: Prefix Sum (Optimal)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Compute total sum once, then iterate while maintaining a running left sum. Right sum = total - leftSum - nums[i].

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
