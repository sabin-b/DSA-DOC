# Two Sum II - Input Array Is Sorted

[Problem Link](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/){:target="_blank" rel="noopener noreferrer"}

> **Pattern:** Two Pointers

### Description

Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice. Your solution must use only constant extra space.

!!! example "Test Cases"

    **Example 1:**
    Input: numbers = [2, 7, 11, 15], target = 9
    Output: [1, 2]
    Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

    **Example 2:**
    Input: numbers = [2, 3, 4], target = 6
    Output: [1, 3]
    Explanation: The sum of 2 and 4 is 6. Therefore, index1 = 1, index2 = 3. We return [1, 3].

    **Example 3:**
    Input: numbers = [-1, 0], target = -1
    Output: [1, 2]
    Explanation: The sum of -1 and 0 is -1. Therefore, index1 = 1, index2 = 2. We return [1, 2].

### Approach 1: Brute Force

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

Check every pair of elements with two nested loops. For each `i`, scan all `j > i` and return the 1-indexed positions when the pair sums to the target. This works for any array but is too slow for large inputs.

```typescript
function twoSumBruteForce(numbers: number[], target: number): number[] {
    for (let i = 0; i < numbers.length; i++) {
        for (let j = i + 1; j < numbers.length; j++) {
            if (numbers[i] + numbers[j] === target) {
                return [i + 1, j + 1];
            }
        }
    }

    return [];
}

console.log(twoSumBruteForce([2, 7, 11, 15], 9)); // [1, 2]
console.log(twoSumBruteForce([2, 3, 4], 6));      // [1, 3]
console.log(twoSumBruteForce([-1, 0], -1));       // [1, 2]
```

### Approach 2: Two Pointers

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Since the array is sorted, place `leftIndex` at the start and `rightIndex` at the end. Compute the sum of the two pointers. If it equals the target, return the 1-indexed positions. If the sum is smaller than the target, move `leftIndex` right to increase the sum; otherwise move `rightIndex` left to decrease it.

```typescript
function twoSum(numbers: number[], target: number): number[] {
    let leftIndex = 0;
    let rightIndex = numbers.length - 1;

    while (leftIndex < rightIndex) {
        let sum = numbers[leftIndex] + numbers[rightIndex];

        if (target === sum) {
            return [leftIndex + 1, rightIndex +1];
        } else if (target > sum) {
            leftIndex++;
        } else {
            rightIndex--;
        }
    }

    return [];
}

console.log(twoSum([2, 7, 11, 15], 9)); // [1, 2]
console.log(twoSum([2, 3, 4], 6));      // [1, 3]
console.log(twoSum([-1, 0], -1));       // [1, 2]
```

### Explanation

- The **Brute Force** approach checks all O(n²) combinations with nested loops. It uses O(1) extra space but is too slow for large inputs.
- The **Two Pointers** approach exploits the sorted order to converge on the answer in a single pass, using O(1) extra space. Since exactly one solution is guaranteed, the pointers always meet the target.

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| Two Pointers | O(n) | O(1) |
