# 394. Decode String

## Problem Statement
Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `10⁵`.

## Approach:  Two Stacks

---

We use two stacks:
- countStack to store repeat counts (`k`).
- resultStack to store intermediate decoded strings.

### Digit Handling (`0-9`)
- Build `k` by processing consecutive digits.<br><br>

### Opening Bracket (`[`)
- Push `k` onto `countStack` and the current string onto `resultStack`. 
- Reset `k` and `currentResult` for the next segment.<br><br>

### Closing Bracket (`]`)
- Pop `k` from `countStack` and the last decoded segment from `resultStack`. 
- Repeat `currentResult` `k` times and append that to the previous result.<br><br>

### Character Handling(`a-z`)
- Append normal characters to `currentResult`.<br><br>

---

```cpp
class Solution {
public:
    string decodeString(string s) {
        stack<int> countStack;
        stack<string> resultStack;
        string currentResult = "";
        int k = 0;

        for (char c : s) {
            if (isdigit(c)) {
                k = k * 10 + (c - '0');

            } else if (c == '[') {
                countStack.push(k);
                resultStack.push(currentResult);
                k = 0;
                currentResult = "";

            } else if (c == ']') {
                int repeatCount = countStack.top();
                countStack.pop();
                string decodedSegment = resultStack.top();
                resultStack.pop();

                while (repeatCount--) {
                    decodedSegment += currentResult;
                }
                currentResult = decodedSegment;

            } else {
                currentResult += c;
            }
        }
        return currentResult;
    }
};
```

## Complexity
- Time Complexity: 𝑂(𝑛) 
    - Each character is processed exactly once. 
    - Stack operations (`push/pop`) are 𝑂(1).

- Space Complexity: 𝑂(𝑛) 
    - Worst-case: deeply nested structures require storing intermediate results in stacks.

## Conclusion
Uses a stack to decode nested patterns in a structured string format, reconstructing the original message.