## 235	Lowest Common Ancestor of a Binary Search Tree

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

## Solution

递归的思想：
1. 如果p或者q中有一个节点的val等于跟节点的val，则该根节点就是公共祖先。
2. 如果root恰好在p和q的中间，则root是公共祖先。
3. 如果root比p，q的val都大，则公共祖先在左子树
4. 如果root比p，q的val都小，则公共祖先在右子树

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root -> val == p-> val || root -> val == q -> val) return root;
        if(root -> val > min(p->val, q->val) && root -> val < max(p->val, q->val)) return root;
        if(root -> val > max(p->val, q->val))
            return lowestCommonAncestor(root ->left, p, q);
        else
            return lowestCommonAncestor(root -> right, p, q);
    }
};
```