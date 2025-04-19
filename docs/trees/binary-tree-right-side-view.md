# 199. Binary Tree Right Side View

## Problem Statement
Given the `root` of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

---

## Approach: Using Breadth First Search

We can perform a level-order traversal (or Breadth-First Search) on the binary tree. At each level, the rightmost node is the one visible from the right side view.

### Queue and Level Processing:

- A queue is used to traverse nodes level by level.

- At each level, the last node in the queue is the rightmost node visible from that level.

### Edge Cases:  

- If the tree is empty (`root == nullptr`), return an empty vector.

### Final Result:

- The `result` vector contains the values of the rightmost nodes of all levels, ordered from top to bottom.  

---

## Code (C++)

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> result; 
        if (!root) return result; 
            
        queue<TreeNode*> q; 
        q.push(root); 

        while (!q.empty()) {
            int levelSize = q.size();
            TreeNode* rightmost = nullptr;

            for (int i = 0; i < levelSize; i++) {
                TreeNode* currentNode = q.front();
                q.pop();

                rightmost = currentNode;

                if (currentNode->left) q.push(currentNode->left);
                if (currentNode->right) q.push(currentNode->right);                    
            }

            result.push_back(rightmost->val);                
        }
        
        return result;
    }
};
```

## Complexity
- Time: 𝑂(𝑛), where 𝑛 is the number of nodes in the tree. Each node is visited once.

- Space: 𝑂(𝑤), where 𝑤 is the maximum width of the tree (the number of nodes at the largest level).

## Conclusion
This implementation efficiently uses BFS to gather the rightmost node at each level, producing the desired view with linear time and space complexity.