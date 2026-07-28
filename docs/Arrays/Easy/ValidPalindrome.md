# Valid Palindrome

[Problem Link](https://leetcode.com/problems/valid-palindrome/){:target="_blank" rel="noopener noreferrer"}

### Description

A phrase is a **palindrome** if, after converting all uppercase letters to lowercase and removing all non-alphanumeric characters, it reads the same forwards and backwards. Alphanumeric characters include letters (A-Z, a-z) and digits (0-9).

Given a string `s`, return `true` if it is a **palindrome**, or `false` otherwise.

!!! example "Test Cases"

    **Example 1:**
    Input: s = "A man, a plan, a canal: Panama"
    Output: true
    Explanation: "amanaplanacanalpanama" is a palindrome.

    **Example 2:**
    Input: s = "race a car"
    Output: false
    Explanation: "raceacar" is not a palindrome.

    **Example 3:**
    Input: s = " "
    Output: true
    Explanation: After removing non-alphanumeric characters, s is an empty string `""` which reads the same forwards and backwards.

### Approach 1: Two Pointers

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Filter alphanumeric characters and use two pointers from both ends to check if the string reads the same forwards and backwards.

```typescript
function isPalindrome(s: string): boolean {
  let input = "";

  for (let j = 0; j < s.length; j++) {
    if (/[a-zA-Z0-9]/g.test(s[j])) {
      input += s[j].toLowerCase();
    }
  }

  let right = input.length - 1;
  let left = 0;
  while (left < right) {
    if (input[left] !== input[right]) return false;
    left++;
    right--;
  }

  return true;
}

console.log(isPalindrome("A man, a plan, a canal: Panama")); // true
console.log(isPalindrome(" ")); // true
```

### Approach 2: Brute Force (Reverse String)

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Build the reverse of the filtered string and compare directly.

```typescript
function isPalindrome(s: string): boolean {
  let input = "";

  for (let j = 0; j < s.length; j++) {
    if (/[a-zA-Z0-9]/g.test(s[j])) {
      input += s[j].toLowerCase();
    }
  }

  let n = input.length;
  let reverse = "";
  for (let i = n - 1; i >= 0; i--) {
    reverse += input[i];
  }
  return input === reverse;
}

console.log(isPalindrome("A man, a plan, a canal: Panama")); // true
console.log(isPalindrome(" ")); // true
```
