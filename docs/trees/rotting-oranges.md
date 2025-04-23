# 994. Rotting Oranges

## Problem Statement
You are given an `m x n` `grid` where each cell can have one of three values:
- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.
Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.
Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return `-1`.

---

## Approach: Using Breadth First Search

We can use Breadth-First Search (BFS) to simulate the rotting process of the oranges.

### BFS Traversal:

- BFS allows rotting to propagate minute by minute, in all four directions, matching the problem’s requirement.

### Tracking Time:

- Each level of BFS represents one minute passing. We increment `minutes` after processing each level.

### Edge Cases:

- If there are no fresh oranges from the start, return `0`.

- If some fresh oranges cannot be reached, return `-1`.

---

## Code (C++)

```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        queue<pair<int, int>> q;
        int freshCount = 0;
        int minutes = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) {
                    q.push({i, j}); 
                } else if (grid[i][j] == 1) {
                    freshCount++;
                }
            }
        }
            
        vector<pair<int, int>> directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        while (!q.empty() && freshCount > 0) {
            int levelSize = q.size();
            for (int i = 0; i < levelSize; i++) {
                auto [x, y] = q.front();
                q.pop();

                for (auto [dx, dy] : directions) {
                    int nx = x + dx;
                    int ny = y + dy;

                    if (nx >= 0 && ny >= 0 && nx < m && ny < n && grid[nx][ny] == 1) {
                        grid[nx][ny] = 2;
                        q.push({nx, ny});
                        freshCount--;
                    }
                }
            }
            minutes++;
        }

        return freshCount == 0 ? minutes : -1;
    }
};
```

## Complexity
- Time: 𝑂(𝑚 × 𝑛), every cell is visited at most once.

- Space: 𝑂(𝑚 × 𝑛), space used by the queue and auxiliary structures like the `directions` vector.

## Conclusion
This BFS-based solution effectively simulates the rotting process and determines the minimum time required or detects when it’s impossible to rot all oranges.