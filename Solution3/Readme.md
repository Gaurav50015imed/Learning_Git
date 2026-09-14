# Longest Substring Without Repeating Characters

## Problem Description
Given a string `s`, find the length of the longest substring without duplicate characters.

### Examples

* **Example 1:**
  * **Input:** `s = "abcabcbb"`
  * **Output:** `3`
  * **Explanation:** The answer is "abc", with the length of 3. Note that "bca" and "cab" are also correct answers.

* **Example 2:**
  * **Input:** `s = "bbbbb"`
  * **Output:** `1`
  * **Explanation:** The answer is "b", with the length of 1.

* **Example 3:**
  * **Input:** `s = "pwwkew"`
  * **Output:** `3`
  * **Explanation:** The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

### Constraints
* `0 <= s.length <= 10^5`
* `s` consists of English letters, digits, symbols and spaces.

---

## Solution

### Approach: Sliding Window & Hash Map
We can use a "sliding window" to represent the current substring without repeating characters. The window is defined by two pointers: a `left` pointer for the start of the substring and a `right` pointer that iterates through the string.

We use a Hash Map (dictionary) to store the most recent index of each character we encounter. As the `right` pointer moves, if we see a character that is already in our map **and** its recorded index is within our current window (i.e., greater than or equal to `left`), it means we have found a duplicate. To remove the duplicate from our window, we immediately jump the `left` pointer to the position just after the duplicate character's last seen index. We then update the character's index in the map and calculate the maximum length seen so far.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        char_map = {}
        left = 0
        max_length = 0
        
        for right, char in enumerate(s):
            # If we've seen the character and it's inside our current window
            if char in char_map and char_map[char] >= left:
                # Move the left bound to right after the last occurrence
                left = char_map[char] + 1
            
            # Update the character's latest index
            char_map[char] = right
            
            # Update max length found so far
            max_length = max(max_length, right - left + 1)
            
        return max_length
