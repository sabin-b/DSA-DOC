# Merge Sorted Array

[Problem Link](https://leetcode.com/problems/merge-sorted-array/){:target="_blank" rel="noopener noreferrer"}

### Description

You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums2` into `nums1` as one sorted array. The final sorted array should be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to 0 and should be ignored. `nums2` has a length of `n`.

!!! example "Test Cases"

    **Example 1:**
    Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
    Output: [1,2,2,3,5,6]
    Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
    The result of the merge is [1,2,2,3,5,6].

    **Example 2:**
    Input: nums1 = [1], m = 1, nums2 = [], n = 0
    Output: [1]
    Explanation: The arrays we are merging are [1] and [].
    Since nums1 has only one element, no merge is needed.

    **Example 3:**
    Input: nums1 = [0], m = 0, nums2 = [1], n = 1
    Output: [1]
    Explanation: The arrays we are merging are [] and [1].
    Since nums1 is empty, we copy nums2 into nums1.

### Approach 1: Three Pointers (Merge from End)

- **Time Complexity:** O(m + n)
- **Space Complexity:** O(1)

This approach leverages the fact that `nums1` has extra space at the end. Instead of shifting elements, we fill from the back:

1. Start three pointers at the end of their respective arrays:
   - `p1` points to the last valid element in `nums1` (index `m - 1`)
   - `p2` points to the last element in `nums2` (index `n - 1`)
   - `i` points to the last position in `nums1` (index `m + n - 1`)

2. Compare elements from both arrays and place the larger one at position `i`
3. Continue until all elements from `nums2` are placed

```typescript
function merge(
  nums1: number[],
  m: number,
  nums2: number[],
  n: number,
): number[] {
  // Start from the end of both arrays
  let p1 = m - 1;        // Last valid element in nums1
  let p2 = n - 1;        // Last element in nums2
  for (let i = nums1.length - 1; i >= 0; i--) {
    // If nums2 is exhausted, no more merges needed
    if (p2 < 0) break;
    
    // Place the larger element at position i
    if (p1 >= 0 && nums1[p1] > nums2[p2]) {
      nums1[i] = nums1[p1];
      p1--;
    } else {
      nums1[i] = nums2[p2];
      p2--;
    }
  }
  return nums1;
}

console.log(merge([1, 2, 3, 0, 0, 0], 3, [2, 5, 6], 3)); // [1, 2, 2, 3, 5, 6]
console.log(merge([1], 1, [], 0)); // [1]
console.log(merge([0], 0, [1], 1)); // [1]
```