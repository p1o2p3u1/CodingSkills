## Sum Root to Leaf Numbers
Given a binary tree containing digits from `0-9` only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path `1->2->3` which represents the number `123`.

Find the total sum of all root-to-leaf numbers.

For example,
```
    1
   / \
  2   3
```
The root-to-leaf path `1->2` represents the number `12`.
The root-to-leaf path `1->3` represents the number `13`.

Return the `sum = 12 + 13 = 25`.

## Solution
递归版
```
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
private:
    int dfs(TreeNode *x, int sum){
        if(x == NULL) return 0;
        int tmp = sum * 10 + x -> val;
        if(x -> left == NULL && x -> right == NULL) 
            return tmp;
        else
            return dfs(x -> left, tmp) + dfs(x -> right, tmp);
    }
public:
    int sumNumbers(TreeNode *root) {
        return dfs(root, 0);
    }
};
```
非递归版本怎么写……
