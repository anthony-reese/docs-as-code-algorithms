# 236. Lowest Common Ancestor of a Binary Tree

## Problem Statement

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.  
You are given references to the root of a binary tree and two nodes `p` and `q`.  
Return the LCA of nodes `p` and `q`.

---

## Approach: Tree DFS

We use Depth-First Search (DFS) to traverse the tree recursively.

### Base Case:

- If the current node is `nullptr`, we’ve reached a leaf.
- If the current node is equal to `p` or `q`, return it.

### Recursive Search:

- Recursively search the left and right subtrees.

### Combine Results:

- If both left and right return non-null, current node is the LCA.
- If one side is null, return the non-null child.

---

## Code (C++)

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q) {
            return root;
        }

        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        if (left && right) {
            return root;
        }

        return left ? left : right;
    }
};
```

## Complexity
- Time: 𝑂(𝑛), where 𝑛 is the number of nodes in the binary tree.

- Space: 𝑂(ℎ), where ℎ is the height of the binary tree (due to the recursion stack).

## Conclusion
This approach efficiently locates the LCA by leveraging recursive post-order traversal.