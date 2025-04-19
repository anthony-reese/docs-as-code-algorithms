# 8. String to Integer (atoi)

## Problem Statement

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer.

The algorithm for `myAtoi(string s)` is as follows:

1. Whitespace: Ignore any leading whitespace (`" "`).

2. Signedness: Determine the sign by checking if the next character is `'-'` or `'+'`, assuming positivity if neither present.

3. Conversion: Read the integer by skipping leading zeros until a non-digit character is encountered or the end of the string is reached. If no digits were read, then the result is 0.

4. Rounding: If the integer is out of the 32-bit signed integer range `[-2`<sup>`31`</sup>, `2`</sup>`31`</sup>` - 1]`, then round the integer to remain in the range. Specifically, integers less than `-2`</sup>`31`</sup> should be rounded to -231, and integers greater than `2`</sup>`31`</sup>` - 1` should be rounded to `2`</sup>`31`</sup>` - 1`.
Return the integer as the final result.

---

## Approach: String Manipulation

The `myAtoi()` function converts a string to an integer following the Finite State Machine (FSM) pattern.

### The process consists of five distinct states:

1. Ignore Leading Whitespaces

- Skip all leading spaces using:

```cpp
while (i < n && s[i] == ' ') {
    ++i;
}
```
- Moves to the next state when a non-space character is found.

2. Determine the Sign

- If `s[i] == '+'`, set `sign = 1`.

- If `s[i] == '-'`, set `sign = -1`.

- Move to the next character.

3. Convert Digits to an Integer

- If `isdigit(s[i])`, accumulate the number:

```cpp
result = result * 10 + (s[i] - '0');
```

- If a non-digit is found, stop processing.

4. Handle Overflow

- Since `result` is of type `long long`, we check:

```cpp
if (result * sign > INT_MAX) return INT_MAX;
if (result * sign < INT_MIN) return INT_MIN;
```

- This clamps the number within the 32-bit integer range.

5. Return the Final Value

- Multiply `result` by `sign` and return the integer.

---

## Code (C++)

```cpp
class Solution {
    public:
        int myAtoi(string s) {
            int i = 0, n = s.length();

            while (i < n && s[i] == ' ') {
                ++i;
            }
            
            int sign = 1;
            if (i < n && (s[i] == '-' || s[i] == '+')) {
                sign = (s[i] == '-') ? -1 : 1;
                ++i;
            }

            long long result = 0;
            while (i < n && isdigit(s[i])) {
                result = result * 10 + (s[i] - '0');
                
                if (result * sign > INT_MAX) return INT_MAX;
                if (result * sign < INT_MIN) return INT_MIN;
                ++i;
            }
            return result * sign;
        }
    };
```

## Complexity
- Time Complexity: 𝑂(𝑛) — The function processes each character in the string at most once, and the while loops iterate through the string linearly, where n is the length of the input string.

- Space Complexity: 𝑂(1) — The function does not use extra space that grows with the input size, only using a few integer variables.

## Conclusion
This method accurately parses and clamps the string into a valid 32-bit integer using efficient linear processing.