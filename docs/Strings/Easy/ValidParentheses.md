# Valid Parentheses

[Problem Link](https://leetcode.com/problems/valid-parentheses/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

!!! example "Test Cases"

    Example 1:
    Input: s = "()"
    Output: true

    Example 2:
    Input: s = "()[]{}"
    Output: true

    Example 3:
    Input: s = "(]"
    Output: false

    Example 4:
    Input: s = "([)]"
    Output: false
    Explanation: Open bracket not closed in correct order.

    Example 5:
    Input: s = "{[]}"
    Output: true

### Approach: Stack

- Time Complexity: O(n)
- Space Complexity: O(n)

Use a stack to keep track of opening brackets. When encountering a closing bracket, check if it matches the most recent opening bracket.

```typescript
function isPair(last: string, curr: string): boolean {
  return (
    (last === "{" && curr === "}") ||
    (last === "(" && curr === ")") ||
    (last === "[" && curr === "]")
  );
}

function isValid(s: string): boolean {
  let stack: string[] = [];
  for (let index = 0; index < s.length; index++) {
    const curr = s[index];
    const last = stack[stack.length - 1];
    if (stack.length > 0 && last !== undefined && isPair(last, curr)) {
      stack.pop();
    } else {
      stack.push(curr);
    }
  }
  return stack.length === 0;
}

// Example usage
console.log(isValid("()[]{}"));  // true
console.log(isValid("(]"));       // false
console.log(isValid("([)]"));      // false
console.log(isValid("{[]}"));     // true
```

### Explanation

1. **Initialize an empty stack** to track unmatched opening brackets.
2. **Iterate through each character** in the string:
   - If it's an opening bracket `(`, `{`, `[`, push it onto the stack.
   - If it's a closing bracket `)`, `}`, `]`, check if the stack's top matches the corresponding opening bracket. If yes, pop the stack; otherwise, the string is invalid.
3. **Return true** if the stack is empty (all brackets matched), otherwise false.