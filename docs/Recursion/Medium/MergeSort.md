# Merge Sort

[Problem Link](https://leetcode.com/problems/sort-an-array/){:target="_blank" rel="noopener noreferrer"}

### Description

Write a recursive function to sort an array of numbers using the **Merge Sort** technique.

Merge Sort follows the divide-and-conquer idea:

- Divide the array into two halves.
- Recursively sort both halves.
- Merge the two sorted halves into one sorted array.

!!! example "Test Cases"

    **Example 1:**
    Input: arr = [2, 1, 3, 8, 6, 5, 4, 10]
    Output: [1, 2, 3, 4, 5, 6, 8, 10]
    Explanation: The array is split into smaller parts, each part is sorted, and then all parts are merged back in sorted order.

    **Example 2:**
    Input: arr = [5, 2, 4, 1]
    Output: [1, 2, 4, 5]
    Explanation: After recursively splitting and merging, the final array becomes sorted.

    **Example 3:**
    Input: arr = [7]
    Output: [7]
    Explanation: A single-element array is already sorted.

### Approach 1: Recursion + Merge

- **Time Complexity:** O(n log n) - The array is split into `log n` levels, and each level processes all `n` elements during merging.
- **Space Complexity:** O(n) - Extra arrays are used while merging, and the recursion stack adds additional overhead.

This approach uses recursion to keep breaking the problem into smaller subproblems.

- **Base Case:** If the array length is `0` or `1`, it is already sorted, so we return it directly.
- **Recursive Step:** Split the array into two halves, recursively sort both halves, and merge them into one sorted array.

The `merge` function is the key helper here. Since both halves are already sorted, we can compare their front elements one by one and build the final sorted result efficiently.

```typescript
function mergeSort(arr: number[]): number[] {
  // Stop when the array is already sorted by size.
  if (arr.length <= 1) return arr;

  // Split the array into left and right halves.
  const middle = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, middle));
  const right = mergeSort(arr.slice(middle));

  // Merge the two sorted halves into one sorted array.
  return merge(left, right);
}

function merge(left: number[], right: number[]): number[] {
  // Store the merged sorted values here.
  const result: number[] = [];

  // Track the current position in both halves.
  let i = 0;
  let j = 0;

  // Compare current elements and push the smaller one first.
  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) {
      result.push(left[i]);
      i++;
    } else {
      result.push(right[j]);
      j++;
    }
  }

  // Add any remaining values from the left half.
  while (i < left.length) {
    result.push(left[i]);
    i++;
  }

  // Add any remaining values from the right half.
  while (j < right.length) {
    result.push(right[j]);
    j++;
  }

  return result;
}

console.log(mergeSort([2, 1, 3, 8, 6, 5, 4, 10])); // [1, 2, 3, 4, 5, 6, 8, 10]
```

### Question and Answer Flow

**Q1: Why do we return immediately when the array length is 0 or 1?**  
Because an empty array or a single-element array is already sorted. This is the base case that stops recursion.

**Q2: Why do we split the array into two halves?**  
Because sorting a smaller array is easier to manage recursively. Merge Sort keeps reducing the problem size until it becomes simple enough to solve directly.

**Q3: Why do we recursively sort both halves first?**  
Because the merge step only works correctly when both halves are already sorted.

**Q4: Why does the merge step use two pointers?**  
Because we need to compare the current smallest remaining values from both halves and place the smaller one into the result array.

**Q5: What happens after one half is fully used?**  
We append the remaining elements from the other half because they are already sorted.

**Q6: Why is Merge Sort efficient?**  
Because it divides the problem into balanced halves and processes all elements in a structured way at each level, giving a time complexity of O(n log n).

### Mind Map

```mermaid
mindmap
  root((Merge Sort))
    Base Case
      Array length <= 1
      Return as it is
    Divide
      Find middle index
      Split into left half
      Split into right half
    Conquer
      Sort left recursively
      Sort right recursively
    Merge
      Compare left[i] and right[j]
      Push smaller value
      Append remaining elements
    Result
      Final sorted array
    Complexity
      Time O(n log n)
      Space O(n)
```
