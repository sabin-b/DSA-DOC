# Product of Array Except Self

[Problem Link](https://leetcode.com/problems/product-of-array-except-self/){:target="_blank" rel="noopener noreferrer"}

> **Pattern:** Prefix/Suffix Products | **Retrack Date:** 09/07/2026

### Description

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of `nums` is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [1, 2, 3, 4]
    Output: [24, 12, 8, 6]

    **Example 2:**
    Input: nums = [-1, 1, 0, -3, 3]
    Output: [0, 0, 9, 0, 0]

### Approach 1: Brute Force

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

For each element, iterate through the entire array and multiply all elements except the current one. Store the result in the answer array.

```typescript
function productExceptSelf(nums: number[]): number[] {
  let numsLength = nums.length;
  let ans = new Array(numsLength);

  for (let i = 0; i < numsLength; i++) {
    let sum = 1;
    for (let j = 0; j < numsLength; j++) {
      if (j !== i) sum = sum * nums[j];
    }
    ans[i] = sum;
  }

  return ans;
}

console.log(productExceptSelf([1, 2, 3, 4])); // [24, 12, 8, 6]
console.log(productExceptSelf([0, 0])); // [0, 0]
```

### Approach 2: Prefix and Suffix Products

- **Time Complexity:** O(n)
- **Space Complexity:** O(1) (excluding output array)

Use two passes: first compute prefix products (product of all elements to the left), then multiply by suffix products (product of all elements to the right) in a single backward pass.

```typescript
function productExceptSelf(nums: number[]): number[] {
    const n = nums.length;
    const ans = new Array<number>(n);

    // prefix products: ans[i] = product of nums[0..i-1]
    ans[0] = 1;
    for (let i = 1; i < n; i++) {
        ans[i] = ans[i - 1] * nums[i - 1];
    }

    // suffix product and combine with prefix
    let suffix = 1;
    for (let i = n - 1; i >= 0; i--) {
        ans[i] = ans[i] * suffix;
        suffix *= nums[i];
    }

    return ans;
}

console.log(productExceptSelf([1, 2, 3, 4])); // [24, 12, 8, 6]
console.log(productExceptSelf([0, 0])); // [0, 0]
```

### Explanation

- The **Brute Force** approach checks all O(n²) combinations with a nested loop. It uses O(1) extra space but is too slow for large inputs.
- The **Prefix and Suffix Products** approach uses two passes: left-to-right for prefix products, then right-to-left to multiply suffix products. This avoids division and achieves O(n) time with O(1) extra space.

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| Prefix and Suffix Products | O(n) | O(1) |
