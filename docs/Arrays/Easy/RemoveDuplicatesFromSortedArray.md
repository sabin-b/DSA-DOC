# Remove Duplicates from Sorted Array

[Problem Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

### Description

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` after placing the final result in the first `k` slots of `nums`.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [1,1,2]
    Output: 2, nums = [1,2,_]
    Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
    It does not matter what you leave beyond the returned k (hence they are underscores).

    **Example 2:**
    Input: nums = [0,0,1,1,1,2,2,3,3,4]
    Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
    Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
    It does not matter what you leave beyond the returned k (hence they are underscores).

### Approach 1: Two Pointers

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach uses a "two-pointer" technique. One pointer (`i`) iterates through the array, and another pointer (`writeIndex`) keeps track of the position where the next unique element should be placed.

When `nums[i]` is greater than `nums[writeIndex]`, it means we've found a new unique element. We then increment `writeIndex` and copy the value of `nums[i]` to this new position.

```typescript
function removeDuplicates(nums: number[]): number {
  if (nums.length === 0) {
    return 0;
  }
  let writeIndex = 0;
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] > nums[writeIndex]) {
      nums[++writeIndex] = nums[i];
    }
  }
  return writeIndex + 1;
}

// Example 1
let nums1 = [1, 1, 2];
let k1 = removeDuplicates(nums1);
console.log(k1); // 2
console.log(nums1.slice(0, k1)); // [1, 2]

// Example 2
let nums2 = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4];
let k2 = removeDuplicates(nums2);
console.log(k2); // 5
console.log(nums2.slice(0, k2)); // [0, 1, 2, 3, 4]
```
