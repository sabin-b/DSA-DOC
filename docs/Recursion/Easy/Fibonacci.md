# Fibonacci

### Description

Write a function to return the `n`th Fibonacci number.

The Fibonacci sequence starts with `0` and `1`, and every next number is the sum of the previous two numbers.

!!! example "Test Cases"

    **Example 1:**
    Input: n = 0
    Output: 0
    Explanation: The 0th Fibonacci number is 0.

    **Example 2:**
    Input: n = 1
    Output: 1
    Explanation: The 1st Fibonacci number is 1.

    **Example 3:**
    Input: n = 10
    Output: 55
    Explanation: The sequence is 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55.

### Approach 1: Recursion

- **Time Complexity:** O(2^n) - Each call branches into two more calls, so the work grows exponentially.
- **Space Complexity:** O(n) - The deepest chain of recursive calls can go up to `n` levels.

This approach directly follows the Fibonacci definition.

- **Base Case:** If `n` is `0` or `1`, return `n`.
- **Recursive Step:** Otherwise, return the sum of the previous two Fibonacci numbers.

This is easy to understand, but it repeats the same calculations many times, so it becomes slow for larger values of `n`.

```typescript
function fibnacci(n: number): number {
  // Stop when we reach the first two Fibonacci numbers.
  if (n <= 1) {
    return n;
  }

  // Build the answer from the two previous positions.
  return fibnacci(n - 1) + fibnacci(n - 2);
}

console.log(fibnacci(10)); // 55
```

### Approach 2: Iterative with Array

- **Time Complexity:** O(n) - We calculate each Fibonacci number once from `2` to `n`.
- **Space Complexity:** O(n) - The array stores every Fibonacci value up to index `n`.

This approach avoids repeated recursion by building the sequence from left to right.

- Start with the known values `0` and `1`.
- Use a loop to fill each next position as the sum of the two previous positions.
- Return the value stored at index `n`.

This is much faster than plain recursion and is easier to trace for larger inputs.

```typescript
function fibonacciIterative(n: number): number {
  // Seed the sequence with the first two known values.
  const result = [0, 1];

  // Fill each next Fibonacci value from the two previous ones.
  for (let i = 2; i <= n; i++) {
    result[i] = result[i - 1] + result[i - 2];
  }

  // Return the requested position from the built sequence.
  return result[n];
}

console.log(fibonacciIterative(10)); // 55
```
