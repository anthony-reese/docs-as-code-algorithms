# 139. Word Break

## Problem Statement
Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

---

## Approach: Dynamic Programming

We use dynamic programming (DP) to determine whether the string `s` can be segmented into valid dictionary words.

### Dictionary Lookup:

- To speed up checking if a word exists in `wordDict`, we use an unordered set (`dict`) for 𝑂(1) lookups.

### Dynamic Programming: 

- The outer loop iterates over the length of `s` (`i`), and the inner loop iterates over potential split points (`j`) in the substring `s[0:i]`.

### Efficient Substring Matching:

- For each `i` and `j`, check if `s[j:i]` is in `wordDict` and if `dp[j]` is `true`.   

### Final Result:

- If `dp[n]` is `true`, the string `s` can be segmented; otherwise, the string cannot.

---

## Code (C++)

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> dict(wordDict.begin(), wordDict.end());
        int n = s.size();

        vector<bool> dp(n + 1, false);
        dp[0] = true;

        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.count(s.substr(j, i - j))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        
        return dp[n];
    }
};
```
## Complexity
- Time Complexity:
    - 𝑂(𝑛<sup>2</sup>+𝑚), where 𝑛 is the length of `s` and 𝑚 is the total number of characters in `wordDict` (building the set).

    - The nested loops result in 𝑂(𝑛<sup>2</sup>), and substring lookups and dictionary checks are 𝑂(1) due to the hash set.

- Space Complexity: 
    - 𝑂(𝑛+𝑚), for the dp array and the dictionary set.

## Conclusion
This method efficiently ensures all possible segmentations are checked systematically.