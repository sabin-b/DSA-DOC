# Move Zeroes

[Problem Link](https://leetcode.com/problems/move-zeroes/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [0,1,0,3,12]
    Output: [1,3,12,0,0]

    **Example 2:**
    Input: nums = [0]
    Output: [0]

### Approach 1: Two Pointers (Swap)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This is a highly efficient in-place solution. It uses two pointers:
- `i` (the read pointer) iterates through the entire array from left to right.
- `write` (the write pointer) marks the position where the next non-zero element should be placed.

When the `i` pointer finds a non-zero element, that element is swapped with the element at the `write` pointer's position, and `write` is incremented. This effectively brings all non-zero elements to the front of the array in their original relative order.

```typescript
function moveZeroes(nums: number[]): number[] {
  let write = 0;
  for (let i = 0; i < nums.length; i++) {
    // If we find a non-zero element
    if (nums[i] !== 0) {
      // Swap it with the element at the 'write' position
      [nums[write], nums[i]] = [nums[i], nums[write]];
      // Move the 'write' pointer forward
      write++;
    }
  }
  return nums;
}

console.log(moveZeroes([0, 1, 0, 3, 12])); // [1, 3, 12, 0, 0]
```

### Approach 2: Overwrite and Fill

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach also uses a two-pointer concept but works in two distinct phases.
1.  **Overwrite:** A `count` pointer is used to track the position for the next non-zero element. The array is iterated, and every non-zero element is moved to the `count` position.
2.  **Fill:** After the first loop, all non-zero elements are at the beginning of the array. The second loop then fills the remainder of the array, from `count` to the end, with zeros.

```typescript
function moveZeroesWithFill(nums: number[]): number[] {
  let count = 0; // Position for the next non-zero element
  
  // Move all non-zero elements to the front
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== 0) {
      nums[count] = nums[i];
      count++;
    }
  }

  // Fill the remaining space with zeros
  for (let j = count; j < nums.length; j++) {
    nums[j] = 0;
  }
  
  return nums;
}

console.log(moveZeroesWithFill([0, 1, 0, 3, 12])); // [1, 3, 12, 0, 0]
```
