# Max Consecutive Ones

[Problem Link](https://leetcode.com/problems/max-consecutive-ones/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given a binary array `nums`, return the maximum number of consecutive `1`'s in the array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [1,1,0,1,1,1]
    Output: 3
    Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

    **Example 2:**
    Input: nums = [1,0,1,1,0,1]
    Output: 2

### Approach 1: Single Pass with Counter

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach iterates through the array a single time, using a `counter` to track the current streak of consecutive ones.

- If the current element is a `1`, we increment the `counter`.
- If the current element is a `0`, it breaks the streak. We then compare the `counter` to our `maxValue` to see if we've found a new maximum, and then reset the `counter` to `0`.

After the loop finishes, we do one final check of `counter` against `maxValue` to account for cases where the array ends with a streak of ones.

```typescript
function findMaxConsecutiveOnes(nums: number[]): number {
  let counter = 0;
  let maxValue = 0;
  for (let i = 0; i < nums.length; i++) {
    let value = nums[i];
    if (value !== 0) {
      counter++;
    } else {
      maxValue = Math.max(counter, maxValue);
      counter = 0;
    }
  }
  // Final check in case the array ends with a streak of 1s
  return Math.max(counter, maxValue);
}

// Example 1
console.log(findMaxConsecutiveOnes([1, 1, 0, 1, 1, 1])); // 3

// Example 2
console.log(findMaxConsecutiveOnes([1, 0, 1, 1, 0, 1])); // 2
```
