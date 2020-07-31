[543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

### Idea

Beside the three step analysis, the only thing needs to be considered is that we need to maintain a global variable to keep track of the maximum diameter of each node, and it is obvious that for each node the maximum diameter would be left + right.

### Pseudocode

```
helper function
// giving last level
int left = recursive to the left
int right = recursive to the right
int maxPath = Math.max(mathPath, left + right)
```

### Implementation

```
class Solution {
    int maxPath = 0;
    public int diameterOfBinaryTree(TreeNode root) {

        helper(root);
        return maxPath;
    }
    public int helper(TreeNode node){
        //base case

        if (node == null){
            return 0;
        }

        // get from lchild and right child
        int leftPath = helper(node.left);
        int rightPath = helper(node.right);

        maxPath = Math.max(maxPath, leftPath + rightPath);

        return Math.max(leftPath,rightPath)  + 1;
    }
}
```
