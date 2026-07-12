# Majority Element

[Problem Link](https://leetcode.com/problems/majority-element/){:target="_blank" rel="noopener noreferrer"}

> **Pattern:** Hash Map / Boyer-Moore Voting | **Retrack Date:** 15/07/2026

### Description

Given an array `nums` of size `n`, return the majority element.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [3, 2, 3]
    Output: 3

    **Example 2:**
    Input: nums = [2, 2, 1, 1, 1, 2, 2]
    Output: 2

### Approach 1: Hash Map

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Use a hash map to count the frequency of each element. Iterate through the array and populate the map. Then find the key with the maximum count and return it.

```typescript
function majorityElement(nums: number[]): number {
  let map = new Map<number, number>();

  for (let i = 0; i < nums.length; i++) {
    if (map.has(nums[i])) map.set(nums[i], (map.get(nums[i]) ?? 0) + 1);
    else map.set(nums[i], 1);
  }

  let maxCountVal = 0;
  let element = 0;

  for (const [key, value] of map) {
    if (value > maxCountVal) {
      maxCountVal = value;
      element = key;
    }
  }

  return element;
}

console.log(majorityElement([3, 2, 3]));             // 3
console.log(majorityElement([2, 2, 1, 1, 1, 2, 2])); // 2
```

### Approach 2: Boyer-Moore Voting Algorithm

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This algorithm works by maintaining a `candidate` and a `count`. When `count` is 0, we pick the current element as the new candidate. For each element, increment `count` if it matches the candidate, otherwise decrement. Since the majority element appears more than half the time, it will survive as the candidate after all cancellations.

```typescript
function majorityElement(nums: number[]): number {
  let candidate = 0;
  let count = 0;
  for (let i = 0; i < nums.length; i++) {
    if (count === 0) candidate = nums[i];
    count += nums[i] === candidate ? 1 : -1;
  }
  return candidate;
}

console.log(majorityElement([3, 2, 3,2,3]));             // 3
console.log(majorityElement([2, 2, 1, 1, 1, 2, 2])); // 2
```

### Explanation

- The **Hash Map** approach is straightforward: count frequencies using a map and return the element with the highest count. It is simple and works for any frequency-based problem, but uses O(n) extra space.
- The **Boyer-Moore Voting** algorithm is optimal. It pairs different elements to cancel each other out. Since the majority element occupies more than half the array, it will always be the final surviving candidate. This is done in constant space with a single pass.

| Approach | Time | Space |
|----------|------|-------|
| Hash Map | O(n) | O(n) |
| Boyer-Moore Voting | O(n) | O(1) |
