# 2327. Number of People Aware of a Secret

## Problem Statement
On day `1`, one person discovers a secret.

You are given an integer `delay`, which means that each person will share the secret with a new person every day, starting from `delay` days after discovering the secret. You are also given an integer `forget`, which means that each person will forget the secret `forget` days after discovering it. A person cannot share the secret on the same day they forgot it, or on any day afterwards.

Given an integer n, return the number of people who know the secret at the end of day `n`. Since the answer may be very large, return it modulo `10`<sup>`9`</sup>` + 7`.

---

## Approach: Dynamic Programming

We use Dynamic Programming (DP) to efficiently track secret sharing.

### DP Array Initialization

- `dp[i]` stores the number of people who learn the secret on Day `i`.

- Initially, `dp[1] = 1` (since only one person knows the secret on Day 1).

### Simulating Secret Sharing

- For each day `curDay`, if people learn the secret on that day, they will:

    - Start sharing from `curDay + delay`.

    - Stop sharing by `curDay + forget - 1`.

- Update `dp[nextDay]` to track newly aware people.

### Final Count of Aware People

- Sum up all `dp[i]` values for the last `forget` days (since others have forgotten).<br><br>

---

## Code (C++)

```cpp
class Solution {
    public:
        int peopleAwareOfSecret(int n, int delay, int forget) {
            const int MOD = 1e9 + 7;
    
            vector<int> dp(n + 1, 0);
            dp[1] = 1;
    
            for (int curDay = 1; curDay <= n; ++curDay) {
                if (dp[curDay] > 0) {
                    for (int nextDay = curDay + delay; nextDay < curDay + forget && nextDay <= n; ++nextDay) {
                        dp[nextDay] = (dp[nextDay] + dp[curDay]) % MOD;
                    }
                }
            }
            
            int result = 0;
            for (int day = n - forget + 1; day <= n; ++day) {
                if (day >= 1) {
                    result = (result + dp[day]) % MOD;
                }
            }
    
            return result;
        }
    };
```
## Complexity
- Time Complexity: 𝑂(𝑛 * forget) - Nested loops update future days.

- Space Complexity: 𝑂(𝑛) - Stores DP array.

## Conclusion
Tracks secret spread and expiration using dynamic programming.