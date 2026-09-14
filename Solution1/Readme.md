# Two Sum

## Problem Description
You are given an array of integers `nums` and an integer `target`. Return the indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice. You can return the answer in any order.

### Examples

* **Example 1:**
  * **Input:** `nums = [2,7,11,15]`, `target = 9`
  * **Output:** `[0,1]`
  * **Explanation:** Because `nums[0] + nums[1] == 9`, we return `[0, 1]`.

* **Example 2:**
  * **Input:** `nums = [3,2,4]`, `target = 6`
  * **Output:** `[1,2]`

* **Example 3:**
  * **Input:** `nums = [3,3]`, `target = 6`
  * **Output:** `[0,1]`

### Constraints
* `2 <= nums.length <= 10^4`
* `-10^9 <= nums[i] <= 10^9`
* `-10^9 <= target <= 10^9`
* Only one valid answer exists.

---

## Solution

The primary solution code is located in the file named "solution.py".

### Approach: Brute Force
This implementation uses nested loops to evaluate every possible pair of numbers in the array. The outer loop selects the first number, and the inner loop checks all subsequent numbers to see if their sum matches the `target`. Once the exact match is found, the function returns their respective indices.

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        n = len(nums)
        for i in range(n):
            for j in range(i + 1, n):
                if nums[i] + nums[j] == target:
                    return [i, j] 
        return []
