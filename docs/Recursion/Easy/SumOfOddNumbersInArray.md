# Sum of Odd Numbers in an Array (Recursive)

### Description

Write a recursive function that takes an array of numbers and returns the sum of only the odd numbers within that array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [10, 2, 5, 10, 3]
    Output: 8
    Explanation: The odd numbers are 5 and 3. Their sum is 5 + 3 = 8.

    **Example 2:**
    Input: nums = [1, 2, 3, 4, 5]
    Output: 9
    Explanation: The odd numbers are 1, 3, and 5. Their sum is 1 + 3 + 5 = 9.

    **Example 3:**
    Input: nums = [2, 4, 6, 8]
    Output: 0
    Explanation: There are no odd numbers in the array.

### Approach 1: Recursion from End

- **Time Complexity:** O(n) - The function calls itself for each element in the array.
- **Space Complexity:** O(n) - Each function call adds a frame to the call stack.

This function recursively calculates the sum by starting from the end of the array.
- **Base Case:** When the `index` reaches 0, it checks if the first element is odd and returns it, otherwise returns 0. This stops the recursion.
- **Recursive Step:** At the current `index`, it checks if the number is odd.
    - If it is odd, it adds the number to the result of the recursive call for the rest of the array (`index - 1`).
    - If it is even, it adds 0 to the result of the recursive call.

```typescript
function sumOfOddNumbers(numbers: number[], index: number): number {
  // Base Case: Stop when we've processed the first element.
  if (index === 0) {
    return numbers[0] % 2 !== 0 ? numbers[0] : 0;
  }

  const isOdd = numbers[index] % 2 !== 0;

  // Recursive Step: Add the current number if it's odd, then process the rest of the array.
  return (isOdd ? numbers[index] : 0) + sumOfOddNumbers(numbers, index - 1);
}

const test = [10, 2, 5, 10, 3];
console.log(sumOfOddNumbers(test, test.length - 1)); // 8

const test2 = [1, 2, 3, 4, 5];
console.log(sumOfOddNumbers(test2, test2.length - 1)); // 9
```

---

