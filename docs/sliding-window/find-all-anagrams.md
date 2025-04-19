# 438. Find All Anagrams in a String

## Problem Statement
Given two strings `s` and `p`, return an array of all the start indices of `p`'s anagrams in `s`. You may return the answer in any order.

---

## Approach: Sliding Window

Use a sliding window with frequency counts to track anagrams efficiently.

### Frequency Arrays:

- `count_p` stores the character frequencies of `p`.

- `count_window` tracks the character frequencies in the current window of `s`.

### Initialize the First Window:

- Process the first `p.length()` characters of `s` to initialize `count_window`.

- Compare `count_window` with `count_p`—if they match, store the starting index (`0`).

### Sliding the Window:

- For every new character in `s` (starting from index `p.length()`), adjust `count_window`:
    - Remove the character that is slides out of the window.
    - Add the new character that slides into the window.

- After each adjustment, compare `count_window` and `count_p`. If they match, store the current starting index.

---

## Code (C++)

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> result;
        if (s.length() < p.length()) return result;

        vector<int> count_p(26, 0);
        vector<int> count_window(26, 0);

        for (int i = 0; i < p.length(); i++) {
            count_p[p[i] - 'a']++;
            count_window[s[i] - 'a']++;
        }
        if (count_window == count_p) {
            result.push_back(0);
            }
        for (int i = p.length(); i < s.length(); i++) {
            count_window[s[i - p.length()] - 'a']--;

            count_window[s[i] - 'a']++;
            
            if (count_window == count_p) {
                result.push_back(i - p.length() + 1);
            }
        }   
        return result;
    }
};
```
## Complexity
- Time Complexity: 𝑂(𝑛) — Each character is processed once.

- Space Complexity: 𝑂(1) — The frequency arrays have a fixed size of 26, meaning constant space is used.

## Conclusion
This impletmentation ensures linear time complexity by avoiding repeated sorting or comparisons.