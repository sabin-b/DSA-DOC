# Reverse String

[Problem Link](https://leetcode.com/problems/reverse-string/){:target="_blank" rel="noopener noreferrer"}

### Description

Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array in-place with O(1) extra memory.

!!! example "Test Cases"

    **Example 1:**
    Input: s = ["h","e","l","l","o"]
    Output: ["o","l","l","e","h"]

    **Example 2:**
    Input: s = ["H","a","n","n","a","h"]
    Output: ["h","a","n","n","a","H"]

### Approach 1: Two Pointers

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This is the most common and intuitive approach. We use two pointers, `left` starting at the beginning of the array and `right` at the end. We swap the elements at these pointers and move them towards the center until they meet or cross.

```typescript
function reverseString(s: string[]): void {
  let left = 0;
  let right = s.length - 1;
  while (left < right) {
    // Swap elements
    let temp = s[left];
    s[left] = s[right];
    s[right] = temp;
    
    // Move pointers
    left++;
    right--;
  }
}

// Example
let s1 = ["h","e","l","l","o"];
reverseString(s1);
console.log(s1); // ["o","l","l","e","h"]
```

### Approach 2: Loop to Half

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach iterates from the beginning of the array up to the halfway point. In each iteration, it swaps the element at the current index `i` with the corresponding element from the end of the array, `totalLength - i - 1`.

```typescript
function reverseStringWithHalfLoop(s: string[]): void {
  let totalLength = s.length;
  let halfLength = Math.floor(totalLength / 2);
  for (let i = 0; i < halfLength; i++) {
    // Swap elements
    let temp = s[i];
    s[i] = s[totalLength - i - 1];
    s[totalLength - i - 1] = temp;
  }
}

// Example
let s2 = ["H","a","n","n","a","h"];
reverseStringWithHalfLoop(s2);
console.log(s2); // ["h","a","n","n","a","H"]
```