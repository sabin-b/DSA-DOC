# Sort Colors

[Problem Link](https://leetcode.com/problems/sort-colors/){:target="_blank" rel="noopener noreferrer"}

> **Pattern:** Dutch National Flag / Two Pointers 

### Description

Given an array `nums` with `n` objects colored red, white, or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [2, 0, 2, 1, 1, 0]
    Output: [0, 0, 1, 1, 2, 2]

    **Example 2:**
    Input: nums = [2, 0, 1]
    Output: [0, 1, 2]

### Approach 1: Counting Sort (Two Pass)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Count the occurrences of 0, 1, and 2 in the first pass. In the second pass, overwrite the array with the counted values in order.

```typescript
function sortColors(nums: number[]): void {
    let count0 = 0;
    let count1 = 0;
    let count2 = 0;

    for (let num of nums) {
        if (num === 0) count0++;
        else if (num === 1) count1++;
        else count2++;
    }

    let index = 0;
    while (count0 > 0) {
        nums[index++] = 0;
        count0--;
    }
    while (count1 > 0) {
        nums[index++] = 1;
        count1--;
    }
    while (count2 > 0) {
        nums[index++] = 2;
        count2--;
    }
}
```

### Approach 2: Dutch National Flag (Single Pass)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Use three pointers: `low`, `mid`, and `high`. Elements before `low` are 0, elements after `high` are 2, and `mid` scans through the array. Swap 0s to the front and 2s to the back, leaving 1s in the middle.

```typescript
function sortColors(nums: number[]): void {
    let low = 0;
    let mid = 0;
    let high = nums.length - 1;

    while (mid <= high) {
        if (nums[mid] === 0) {
            [nums[low], nums[mid]] = [nums[mid], nums[low]];
            low++;
            mid++;
        } else if (nums[mid] === 1) {
            mid++;
        } else {
            [nums[mid], nums[high]] = [nums[high], nums[mid]];
            high--;
        }
    }
}
```

### Explanation

- The **Counting Sort** approach makes two passes: first to count each color, then to write them back. Simple and easy to understand but requires two full traversals.
- The **Dutch National Flag** approach partitions the array in a single pass using three pointers. It swaps 0s to the front and 2s to the back while the `mid` pointer scans forward, achieving optimal O(n) time with one pass.

| Approach | Time | Space |
|----------|------|-------|
| Counting Sort | O(n) | O(1) |
| Dutch National Flag | O(n) | O(1) |
