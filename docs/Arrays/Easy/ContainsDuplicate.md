# Contains Duplicate

[Problem Link](https://leetcode.com/problems/contains-duplicate/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [1, 2, 3, 4]
    Output: false
    Explanation: All elements are distinct.

    **Example 2:**
    Input: nums = [1, 2, 3, 1]
    Output: true
    Explanation: The value 1 appears twice.

    **Example 3:**
    Input: nums = [1, 1, 1, 3, 3, 4]
    Output: true
    Explanation: Values 1 and 3 appear more than once.

### Approach: Set Comparison

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

A Set automatically removes duplicate values. If the size of the Set is different from the original array size, there must be duplicates.

```typescript
function containsDuplicate(nums: number[]): boolean {
  return new Set(nums).size !== nums.length;
}

console.log(containsDuplicate([1, 2, 3, 4]));       // false
console.log(containsDuplicate([1, 2, 3, 1]));      // true
console.log(containsDuplicate([1, 1, 1, 3, 3, 4])); // true
```

### Approach 2: Sorting (O(1) Space)

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(1)

Sort the array first, then check if any adjacent elements are equal.

```typescript
function containsDuplicate(nums: number[]): boolean {
  nums.sort((a, b) => a - b);
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] === nums[i - 1]) return true;
  }
  return false;
}

console.log(containsDuplicate([1, 2, 3, 4]));       // false
console.log(containsDuplicate([1, 2, 3, 1]));      // true
console.log(containsDuplicate([1, 1, 1, 3, 3, 4])); // true
```

### Explanation

- Sort the array in-place
- Traverse and check if any adjacent elements are equal
- Time: O(n log n) due to sorting | Space: O(1) extra space

| Approach | Time | Space |
|----------|------|-------|
| Set | O(n) | O(n) |
| Sorting | O(n log n) | O(1) |