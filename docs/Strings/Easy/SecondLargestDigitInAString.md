# Second Largest Digit in a String

[Problem Link](https://leetcode.com/problems/second-largest-digit-in-a-string/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an alphanumeric string `s`, return the second largest numerical digit that appears in `s`.

If there is no second largest digit, return `-1`.

!!! example "Test Cases"

    Example 1:
    Input: s = "dfa12321afd"
    Output: 2
    Explanation: The digits in the string are [1, 2, 3, 2, 1]. The second largest digit is 2.

    Example 2:
    Input: s = "abc1111"
    Output: -1
    Explanation: There is only one distinct digit in the string, so the answer is -1.

### Approach: Single loop with two variables

- Time Complexity: O(n)
- Space Complexity: O(1)

Use one loop to scan the string and keep track of the largest digit and the second largest distinct digit seen so far.

```typescript
function secondHighest(s: string): number {
  if (!s) return -1;

  let max = -1;
  let sec = -1;

  for (let i = 0; i < s.length; i++) {
    const charValue = s.charCodeAt(i);

    if (charValue < 48 || charValue > 57) continue;

    const value = charValue - 48;

    if (value > max) {
      sec = max;
      max = value;
    } else if (value > sec && value < max) {
      sec = value;
    }
  }

  return sec;
}

console.log(secondHighest("dfa12321afd")); // 2
console.log(secondHighest("abc1111")); // -1
```
