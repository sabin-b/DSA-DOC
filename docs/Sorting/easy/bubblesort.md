# Bubble Sort

### Description

Given an array of numbers `arr`, sort the array in ascending order using the bubble sort algorithm and return the sorted array.

Bubble sort repeatedly compares adjacent elements and swaps them when they are in the wrong order. After each pass, the largest unsorted value moves to its correct position at the end of the array.

!!! example "Test Cases"

    **Example 1:**
    Input: arr = [5, 4, 3, 2, 1]
    Output: [1, 2, 3, 4, 5]
    Explanation: Each pass swaps larger values toward the end until the array becomes sorted.

    **Example 2:**
    Input: arr = [1, 2, 3, 4, 5]
    Output: [1, 2, 3, 4, 5]
    Explanation: The array is already sorted, so the algorithm stops early.

    **Example 3:**
    Input: arr = []
    Output: []
    Explanation: An empty array has nothing to sort.

### Approach 1: Optimized Bubble Sort

- **Time Complexity:** O(n^2) in the worst case, O(n) in the best case when the array is already sorted.
- **Space Complexity:** O(1) because sorting is done in place.

This approach compares adjacent elements and swaps them whenever the left value is greater than the right value.

An optimization is used with the `swapped` flag. If no swap happens during a full pass, the array is already sorted, so we can stop early.

```typescript
function bubbleSort(arr: number[]): number[] {
  // Return an empty array when the input is not a valid non-empty array.
  if (!Array.isArray(arr) || !arr.length) return [];

  for (let i = 0; i < arr.length - 1; i++) {
    // Track whether this pass changed anything so we can stop early.
    let swapped = false;

    for (let j = 0; j < arr.length - 1 - i; j++) {
      // Swap adjacent values when they are in the wrong order.
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        swapped = true;
      }
    }

    // Stop when a full pass makes no swaps because the array is sorted.
    if (!swapped) break;
  }

  return arr;
}

console.log(bubbleSort([5, 4, 3, 2, 1])); // [1, 2, 3, 4, 5]
```
