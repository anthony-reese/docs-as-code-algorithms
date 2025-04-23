# 210. Course Schedule II

## Problem Statement
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. 
You are given an array `prerequisites` where `prerequisites[i] = [a`<sub>`i`</sub>`, b`<sub>`i`</sub>`]` indicates that you must take course `b`<sub>`i`</sub> first if you want to take course `a`<sub>`i`</sub>.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take 
course `1`.

Return the ordering of courses you should take to finish all courses. If there are many valid 
answers, return any of them. If it is impossible to finish all courses, return an empty array.

---

## Approach: Using Breadth First Search

To determine the order in which courses can be taken, we can use BFS approach for topological sorting. This problem is essentially a graph problem where courses are nodes and prerequisites are directed edges.

### Graph Construction:

- Represent courses as nodes and prerequisites as directed edges in the graph.

### BFS for Topological Sort:  

- Start with courses that have no prerequisites (in-degree `0`).

- Process these courses, adding their neighbors to the queue when their prerequisites are fulfilled (in-degree becomes `0`).

### Cycle Detection:

- If not all courses are processed, it indicates a cycle in the graph, making it impossible to complete all courses.

---

## Code (C++)

```cpp
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adjList(numCourses);
        vector<int> inDegree(numCourses, 0);

        for (auto& prereq : prerequisites) {
            int course = prereq[0];
            int prerequisite = prereq[1];
            adjList[prerequisite].push_back(course);
            inDegree[course]++;
        }
            
        queue<int> q;
        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] == 0) {
                q.push(i);
            }
        }
            
        vector<int> result;
        while (!q.empty()) {
            int current = q.front();
            q.pop();
            result.push_back(current);

            for (int neighbor : adjList[current]) {
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0) {
                    q.push(neighbor);
                }
            }
        }
            
        if (result.size() == numCourses) {
            return result;
        } else {
            return {};
        }
    }
};
```

## Complexity
Time: 𝑂(𝑉 + 𝐸) 
- Where 𝑉 is the number of courses and 𝐸 is the number of prerequisites. 
- We build the graph in 𝑂(𝐸) and travere the graph in 𝑂(𝑉 + 𝐸).

Space: 𝑂(𝑉 + 𝐸) 
- For the adjacency list and the in-degree tracking.

## Conclusion
This approach efficiently computes the course order or detects if that's impossible to complete all courses due to cyclic dependencies.