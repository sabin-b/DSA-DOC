# Find Disappeared Numbers

[Problem Link](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an array `nums` of `n` integers where `nums` contains all integers in the range `[1, n]`, some elements appear multiple times while others don't appear at all. Return all the integers in the range `[1, n]` that do not appear in the array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [4,3,2,1,6,7]
    Output: [5, 8]
    Explanation: n = 6 since array has 6 elements. Range is [1,6]. Numbers 5 is missing and 8 is beyond range.

    **Example 2:**
    Input: nums = [1,1]
    Output: [2]
    Explanation: n = 2 since array has 2 elements. Range is [1,2]. Number 2 is missing.

    **Example 3:**
    Input: nums = [4,3,2,7,8,2,1,5]
    Output: [6]
    Explanation: n = 8 since array has 8 elements. Range is [1,8]. Number 6 is missing.

### Approach 1: Negative Marking

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

The idea is to use the index as a hash key. For each number `num` in the array, we mark the position at index `|num| - 1` as negative (if not already negative). After first pass, numbers whose indices remain positive indicate the corresponding number is missing from the array.

```typescript
function findDisappearedNumbers(nums: number[]): number[] {
  if (!Array.isArray(nums) || !nums.length) return [];
  
  let N = nums.length;
  for (let i = 0; i < N; i++) {
    let index = Math.abs(nums[i]) - 1;
    if (index >= 0 && index < N && nums[index] > 0) {
      nums[index] = -nums[index];
    }
  }
  
  const result: number[] = [];
  for (let j = 0; j < N; j++) {
    if (nums[j] > 0) result.push(j + 1);
  }
  return result;
}

console.log(findDisappearedNumbers([4, 3, 2, 1, 6, 7])); // [5]
console.log(findDisappearedNumbers([1, 1]));              // [2]
console.log(findDisappearedNumbers([4, 3, 2, 7, 8, 2, 1, 5])); // [6]
```

### Explanation

1. **First pass (marking):** Iterate through each element. Calculate the index position using `Math.abs(nums[i]) - 1`. If that position contains a positive number, negate it to mark that the number is present.

2. **Second pass (finding):** Iterate again. Any index position that still has a positive value indicates the number `index + 1` was never seen in the original array.

| Step | Action |
|------|--------|
| 1 | Use array indices as hash keys |
| 2 | Negate values to mark presence |
| 3 | Collect indices with positive values |

### Approach 2: Cyclic Sort

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Place each number in its correct index position (value - 1). After sorting, iterate and find positions where the number doesn't match the index + 1.

```typescript
function findDisappearedNumbers(nums: number[]): number[] {
  let i = 0;
  while (i < nums.length) {
    let correctIdx = nums[i] - 1;
    if (nums[i] !== nums[correctIdx] && correctIdx >= 0) {
      [nums[i], nums[correctIdx]] = [nums[correctIdx], nums[i]];
    } else {
      i++;
    }
  }

  const result: number[] = [];
  for (let j = 0; j < nums.length; j++) {
    if (nums[j] !== j + 1) result.push(j + 1);
  }
  return result;
}

console.log(findDisappearedNumbers([4, 3, 2, 1, 6, 7])); // [5]
console.log(findDisappearedNumbers([1, 1]));              // [2]
console.log(findDisappearedNumbers([4, 3, 2, 7, 8, 2, 1, 5])); // [6]
```

| Approach | Time | Space |
|----------|------|-------|
| Negative Marking | O(n) | O(1) |
| Cyclic Sort | O(n) | O(1) |