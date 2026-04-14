# Selection Sort

### Description

Given an array of numbers `arr`, sort the array in ascending order using the selection sort algorithm and return the sorted array.

Selection sort divides the array into a sorted and unsorted region. It repeatedly finds the minimum element from the unsorted region and places it at the beginning of the sorted region.

!!! example "Test Cases"

    **Example 1:**
    Input: arr = [5, 4, 3, 2, 1]
    Output: [1, 2, 3, 4, 5]
    Explanation: The algorithm selects the minimum value from the unsorted portion and swaps it with the first unsorted position.

    **Example 2:**
    Input: arr = [1, 2, 3, 4, 5]
    Output: [1, 2, 3, 4, 5]
    Explanation: The array is already sorted, but the algorithm still makes passes (no swaps occur).

    **Example 3:**
    Input: arr = []
    Output: []
    Explanation: An empty array has nothing to sort.

### Approach 1: Selection Sort

- **Time Complexity:** O(n^2) in all cases.
- **Space Complexity:** O(1) because sorting is done in place.

This approach iterates through the array, finding the minimum element in the unsorted portion and swapping it with the element at the current position.

```typescript
function selectionSort(arr: number[]): number[] {
  // Return an empty array when the input is not a valid non-empty array of numbers.
  if (
    !Array.isArray(arr) ||
    arr.some((item) => typeof item !== "number") ||
    !arr.length
  ) {
    return [];
  }

  // Iterate through each position, selecting the minimum from the unsorted region.
  for (let i = 0; i < arr.length - 1; i++) {
    let min = i;

    // Find the index of the minimum element in the remaining unsorted portion.
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) min = j;
    }

    // Swap the minimum element with the current position if they are different.
    if (min === i) continue;
    let temp = arr[i];
    arr[i] = arr[min];
    arr[min] = temp;
  }

  return arr;
}

console.log(selectionSort([5, 4, 3, 2, 1])); // [1, 2, 3, 4, 5]
```
