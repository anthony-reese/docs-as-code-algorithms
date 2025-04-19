# 151. Reverse Words in a String

## Problem Statement
Given an input string `s`, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in `s` will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

---

## Approach:  Two Pointers

Split the string by spaces, filter out empty strings, reverse the list, and join with a single space.

### Trimming Spaces: 

- Remove leading and trailing spaces by finding the first and last non-space characters.

### Splitting Words: 

- Use a `stringstream` to extract words, automatically discarding extra spaces between them.

### Reversing Order: 

- Store the words in a `vector<string>` and use `reverse()` to rearrange them.

### Joining Words: 

- Combines the reversed words back into a single string with only one space between them.

---

```cpp
class Solution {
    public:
        string reverseWords(string s) {
            int left = 0, right = s.size() - 1;
            while (left <= right && s[left] == ' ') left++;
            while (right >= left && s[right] == ' ') right--;
            s = s.substr(left, right - left + 1);

            stringstream ss(s);
            string word;
            vector<string> words;
            while (ss >> word) {
                words.push_back(word);
            }
            
            reverse(words.begin(), words.end());

            string result;
            for (int i = 0; i < words.size(); ++i) {
                if (i > 0) result += " ";
                result += words[i];
            }
            return result;
        }
    };
```

## Complexity

- Time Complexity: 𝑂(𝑛) — We perform a few linear scans over `s` for trimming, splitting, reversing, and joining.

- Space Complexity: 𝑂(𝑛) — A `vector<string>` stores words, and the final output string requires extra space.

## Conclusion
This approach efficiently reverses word order while trimming extra spaces.