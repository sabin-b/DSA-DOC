# Factorial

### Description

Write a recursive function to calculate the factorial of a non-negative integer `n`. The factorial of `n` (denoted as `n!`) is the product of all positive integers less than or equal to `n`.

The factorial of 0 is defined as 1.

!!! example "Test Cases"

    **Example 1:**
    Input: n = 5
    Output: 120
    Explanation: 5! = 5 * 4 * 3 * 2 * 1 = 120

    **Example 2:**
    Input: n = 3
    Output: 6
    Explanation: 3! = 3 * 2 * 1 = 6

    **Example 3:**
    Input: n = 0
    Output: 1
    Explanation: By definition, 0! = 1.

### Approach 1: Recursion

- **Time Complexity:** O(n) - The function calls itself `n` times until it reaches the base case.
- **Space Complexity:** O(n) - Each function call is stored on the call stack, leading to `n` frames in memory.

The factorial function has a natural recursive definition:

- **Base Case:** The factorial of any number less than 1 (including 0) is 1. This is the condition that stops the recursion.
- **Recursive Step:** The factorial of `n` is `n` multiplied by the factorial of `n-1`.

The function repeatedly calls itself with a smaller number (`n-1`) until it hits the base case, at which point the chain of multiplications is resolved.

```typescript
function fact(n: number): number {
  // Base Case: Factorial of 0 or 1 is 1.
  if (n <= 1) {
    return 1;
  }

  // Recursive Step: n * factorial of (n-1)
  return n * fact(n - 1);
}

console.log(fact(5)); // 120
console.log(fact(3)); // 6
console.log(fact(0)); // 1
```
