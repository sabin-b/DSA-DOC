# Sum of First N Numbers

### Description

Write a recursive function that computes the sum of all integers from 1 up to a given non-negative integer `n`.

!!! example "Test Cases"

    **Example 1:**
    Input: n = 5
    Output: 15
    Explanation: 5 + 4 + 3 + 2 + 1 + 0 = 15

    **Example 2:**
    Input: n = 10
    Output: 55
    Explanation: 10 + 9 + ... + 1 + 0 = 55

    **Example 3:**
    Input: n = 0
    Output: 0

### Approach 1: Recursion

- **Time Complexity:** O(n) - The function calls itself `n` times.
- **Space Complexity:** O(n) - Each function call is placed on the call stack, leading to `n` stack frames in memory at the deepest point.

This function works based on a recursive definition of sum:
- **Base Case:** The sum of numbers up to 0 is defined as 0. This stops the recursion.
- **Recursive Step:** The sum of numbers up to `n` is `n` plus the sum of numbers up to `n-1`.

The function continuously calls itself with a decreasing argument (`n-1`) until it reaches the base case (`n === 0`), at which point the results are returned back up the call stack.

```typescript
function sum(n: number): number {
  // Base Case: When n is 0, the recursion stops.
  if (n === 0) {
    return 0;
  }
  
  // Recursive Step: n + the sum of all numbers before it.
  return n + sum(n - 1);
}

console.log(sum(5)); // 15
console.log(sum(10)); // 55
```

This file provides a great foundation for your new recursion section. Let me know if you need help with the `git` commands to commit your new files and directories.
