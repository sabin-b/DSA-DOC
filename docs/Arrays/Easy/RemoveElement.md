# Remove Element

[Problem Link](https://leetcode.com/problems/remove-element/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The order of the elements may be changed. Then return the number of elements in `nums` which are not equal to `val`.

Consider the number of elements in `nums` which are not equal to `val` be `k`. To get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [3,2,2,3], val = 3
    Output: 2, nums = [2,2,_,_]
    Explanation: Your function should return k = 2, with the first two elements of nums being 2.
    It does not matter what you leave beyond the returned k (hence they are underscores).

    **Example 2:**
    Input: nums = [0,1,2,2,3,0,4,2], val = 2
    Output: 5, nums = [0,1,4,0,3,_,_,_]
    Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4. Note that the order of the five elements can be arbitrary.
    It does not matter what you leave beyond the returned k (hence they are underscores).

### Approach 1: Two Pointers

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach uses a two-pointer technique. One pointer (`i`) iterates through the entire array, while a second pointer (`writeIndex`) keeps track of the next position to place an element that is **not** equal to `val`.

When `nums[i]` is not the value to be removed, we place it at the `writeIndex` position and increment `writeIndex`.

```typescript
function removeElement(nums: number[], val: number): number {
  let writeIndex = 0;
  for (let i = 0; i < nums.length; i++) {
    // If the current element is not the value to be removed
    if (nums[i] !== val) {
      // Copy it to the writeIndex position and increment writeIndex
      nums[writeIndex++] = nums[i];
    }
  }
  return writeIndex;
}

// Example 1
let nums1 = [3, 2, 2, 3];
let k1 = removeElement(nums1, 3);
console.log(k1); // 2
console.log(nums1.slice(0, k1)); // [2, 2]

// Example 2
let nums2 = [0, 1, 2, 2, 3, 0, 4, 2];
let k2 = removeElement(nums2, 2);
console.log(k2); // 5
console.log(nums2.slice(0, k2)); // [0, 1, 3, 0, 4]
```