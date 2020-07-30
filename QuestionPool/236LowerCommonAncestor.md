[236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

### Idea

In this question, two cases should be considered:

1. one of them is the descendent of the other
2. they are separated in different subtree

> image placeholder

To think of how the subtree will return the correct position, according to the figure, under the case 2, when left ! = null && right != null, this position will be exactly what we want.

### Pseudocode

```
Separately:
if (left and right both are not null):
    return current level node
if (left or right is null):
    return the one is not null;
if (both null) :
    return null;

ParentToAnother:

Samely, this case has also been satisfied, and the only specific condition is in the base case when one of them is founded, no need to continue the search for the rest of the tree

if (node == a or b) :
    return a or b;

```

### Implementation

public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
// not belong to each other
  
 //base case
//merged with below
/_if (root == null) {
return null;
}_/
  
 if (root == null|| root == p || root == q) {
return root;
}
  
 //get from lchild and rchild
TreeNode left = lowestCommonAncestor(root.left, p, q);
TreeNode right = lowestCommonAncestor( root.right, p, q);
  
 //curr level and return to parent
if (left != null && right != null) {
return root;
}
return left == null ? right : left;
}
