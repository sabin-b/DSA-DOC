# Reverse String

[Problem Link](https://leetcode.com/problems/reverse-string/description/)

### Description

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

!!! example "Test Cases"

    Example 1:
    Input: s = ["h","e","l","l","o"]
    Output: ["o","l","l","e","h"]

    Example 2:
    Input: s = ["H","a","n","n","a","h"]
    Output: ["h","a","n","n","a","H"]

    Example 3:
    Input: s = ["a"]
    Output: ["a"]
    Explanation: Single character array remains unchanged.

    Example 4:
    Input: s = []
    Output: []
    Explanation: Empty array remains unchanged.

    Example 5:
    Input: s = ["a","b"]
    Output: ["b","a"]
    Explanation: Two character array gets swapped.

### Approach 1: Two Pointers

- Time Complexity: O(n)
- Space Complexity: O(1)

```typescript
function reverseString(s: string[]): void {
  let left = 0;
  let right = s.length - 1;

  while (left < right) {
    // Swap characters
    let temp = s[left];
    s[left] = s[right];
    s[right] = temp;

    left++;
    right--;
  }
}

// Example usage
let arr1 = ["h", "e", "l", "l", "o"];
reverseString(arr1);
console.log(arr1); // ["o","l","l","e","h"]

let arr2 = ["H", "a", "n", "n", "a", "h"];
reverseString(arr2);
console.log(arr2); // ["h","a","n","n","a","H"]

// Edge cases
let arr3 = ["a"];
reverseString(arr3);
console.log(arr3); // ["a"] - single character

let arr4: string[] = [];
reverseString(arr4);
console.log(arr4); // [] - empty array

let arr5 = ["a", "b"];
reverseString(arr5);
console.log(arr5); // ["b", "a"] - two characters
```

### Approach 2: Using built-in methods

- Time Complexity: O(n)
- Space Complexity: O(1)

```typescript
function reverseString(s: string[]): void {
  s.reverse();
}

// Example usage
let arr6 = ["h", "e", "l", "l", "o"];
reverseString(arr6);
console.log(arr6); // ["o","l","l","e","h"]

// Edge cases
let arr7 = ["a"];
reverseString(arr7);
console.log(arr7); // ["a"] - single character

let arr8: string[] = [];
reverseString(arr8);
console.log(arr8); // [] - empty array
```
