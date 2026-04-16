# Running Sum of 1D Array

[Problem Link](https://leetcode.com/problems/running-sum-of-1d-array/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an array `nums`, we define a running sum of an array at index `i` as `sum(nums[0]…nums[i])`.

Return the running sum of `nums`.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [1, 2, 3, 4]
    Output: [1, 3, 6, 10]
    Explanation: Running sum is: [1, 1+2, 1+2+3, 1+2+3+4] = [1, 3, 6, 10]

    **Example 2:**
    Input: nums = [1, 1, 1, 1]
    Output: [1, 2, 3, 4]
    Explanation: Running sum is: [1, 2, 3, 4]

    **Example 3:**
    Input: nums = [3, 1, 2, 10, 1]
    Output: [3, 4, 6, 16, 17]

### Approach: In-Place Modification

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

We iterate from index 1 to n-1, and for each position, we add the previous element to the current element. This modifies the array in-place.

```typescript
function runningSum(nums: number[]): number[] {
  for (let i = 1; i < nums.length; i++) {
    nums[i] = nums[i - 1] + nums[i];
  }
  return nums;
}

console.log(runningSum([1, 2, 3, 4]));       // [1, 3, 6, 10]
console.log(runningSum([1, 1, 1, 1]));      // [1, 2, 3, 4]
console.log(runningSum([3, 1, 2, 10, 1]));  // [3, 4, 6, 16, 17]
```

### Explanation

- Start from index 1 (skip index 0 as it's already the running sum)
- For each element at index `i`, add `nums[i-1]` to `nums[i]`
- This works because `nums[i-1]` already contains the sum of all elements from 0 to i-1
- Return the modified array

---

### Approach: Recursive

- **Time Complexity:** O(n)
- **Space Complexity:** O(n) - due to recursive call stack

We use recursion to traverse the array from index 1 to n-1, adding the previous element to the current element at each step.

```typescript
function runningSumRecursive(nums: number[], index: number = 1): number[] {
  if (index >= nums.length) return nums;
  nums[index] = nums[index - 1] + nums[index];
  return runningSumRecursive(nums, index + 1);
}

console.log(runningSumRecursive([1, 2, 3, 4, 5]));  // [1, 3, 6, 10, 15]
```

### Explanation

- Base case: when `index >= nums.length`, return the array
- Recursive case: add `nums[index-1]` to `nums[index]`, then recurse with `index + 1`
- Same logic as iterative approach, just expressed recursively