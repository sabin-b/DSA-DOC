# Subarray Sum Equals K

[Problem Link](https://leetcode.com/problems/subarray-sum-equals-k/){:target="_blank" rel="noopener noreferrer"}

> **Pattern:** Prefix Sum / Hash Map 

### Description

Given an array of integers `nums` and an integer `k`, return the total number of subarrays whose sum equals `k`.

A subarray is a contiguous non-empty sequence of elements within an array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [1, 1, 1], k = 2
    Output: 2
    Explanation: The subarrays [1, 1] (indices 0-1) and [1, 1] (indices 1-2) sum to 2.

    **Example 2:**
    Input: nums = [1, 2, 3], k = 3
    Output: 2
    Explanation: The subarrays [1, 2] (indices 0-1) and [3] (index 2) sum to 3.

### Approach 1: Brute Force

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

Check every possible subarray by iterating through all start and end indices. For each starting index, expand the window while maintaining a running sum. Increment count whenever the running sum equals `k`.

```typescript
function subarraySum(nums: number[]): number {
    const N = nums.length;
    let count = 0;
    for (let i = 0; i < N; i++) {
        let sum = 0;
        for (let j = i; j < N; j++) {
            sum += nums[j];
            if (sum === k) {
                count++;
            }
        }
    }
    return count;
}

console.log(subarraySum([1, 1, 1], 2)); // 2
console.log(subarraySum([1, 2, 3], 3)); // 2
```

### Approach 2: Prefix Sum + Hash Map

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Use a hash map to store the frequency of prefix sums encountered so far. For each element, compute the running prefix sum. If `prefixSum - k` exists in the map, it means there is a subarray ending at the current index that sums to `k`. Initialize the map with `{ 0: 1 }` to handle subarrays that start from index 0.

```typescript
function subarraySum(nums: number[], k: number): number {
    const map = new Map<number, number>();
    map.set(0, 1);
    let count = 0;
    let sum = 0;

    for (let i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (map.has(sum - k)) {
            count += map.get(sum - k)!;
        }
        map.set(sum, (map.get(sum) ?? 0) + 1);
    }

    return count;
}

console.log(subarraySum([1, 1, 1], 2)); // 2
console.log(subarraySum([1, 2, 3], 3)); // 2
```

### Explanation

- The **Brute Force** approach checks all O(n²) subarrays with a nested loop. It uses O(1) extra space but is too slow for large inputs.
- The **Prefix Sum + Hash Map** approach tracks cumulative sums in a single pass. If the same prefix sum appears again, the subarray between the two occurrences sums to zero. By checking `prefixSum - k`, we count subarrays summing to `k` in O(n) time.

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| Prefix Sum + Hash Map | O(n) | O(n) |
