# Sum of All Numbers in an Array (Recursive)

### Description

Write a recursive function that takes an array of numbers and returns the sum of all its elements.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [10, 2, 5, 10, 3]
    Output: 30
    Explanation: 10 + 2 + 5 + 10 + 3 = 30.

    **Example 2:**
    Input: nums = [1, 2, 3, 4, 5]
    Output: 15
    Explanation: 1 + 2 + 3 + 4 + 5 = 15.

### Approach 1: Recursion from End

- **Time Complexity:** O(n) - The function calls itself for each element in the array.
- **Space Complexity:** O(n) - Each function call adds a frame to the call stack.

This function works by breaking the problem down: the sum of an array is the last element plus the sum of the rest of the array.
- **Base Case:** When the `index` reaches 0, it returns the first element. This is the base case that stops the recursion.
- **Recursive Step:** For any other `index`, it returns the number at the current `index` plus the result of the recursive call for the subarray before it (`index - 1`).

```typescript
function sumOfNNumbers(numbers: number[], index: number): number {
  // Base Case: If we're at the first element, just return it.
  if (index === 0) {
    return numbers[0];
  }
  
  // Recursive Step: Return the current element plus the sum of the elements before it.
  return numbers[index] + sumOfNNumbers(numbers, index - 1);
}

const test1 = [10, 2, 5, 10, 3];
console.log(sumOfNNumbers(test1, test1.length - 1)); // 30

const test2 = [1, 2, 3, 4, 5];
console.log(sumOfNNumbers(test2, test2.length - 1)); // 15
```