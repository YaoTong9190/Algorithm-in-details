[297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

### Idea

- BFS  
   Serialize: Using queue to record the tree level by level and adding comma after each word
  Deserialize: split by comma and then restructure the tree level by level

### Pseudocode

```
while (queue is not empty):
    if (left or right is empty)
```

### Implementation

```
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {

        if (root == null) return "";
        String n = "null", sep = ",";
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int size = 0;
        StringBuilder sb = new StringBuilder();
        sb.append(root.val);
        sb.append(sep);
        while(!queue.isEmpty()){
            TreeNode curr = queue.poll();
            if (curr.left != null){
                sb.append(curr.left.val);
                queue.offer(curr.left);
            }
            else{
                sb.append(n);
            }
            sb.append(sep);
            if (curr.right != null){
                sb.append(curr.right.val);
                queue.offer(curr.right);
            }
            else{
                sb.append(n);
            }
            sb.append(sep);
        }
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.isBlank()) return null;
        String[] s = data.split(",");

        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode root = new TreeNode(Integer.parseInt(s[0]));
        queue.offer(root);
        int index = 0;
        while (!queue.isEmpty()){
            TreeNode curr = queue.poll();
            index++;
            if (index < s.length){
                if (s[index].equals("null")){
                    curr.left = null;
                }
                else{
                    curr.left = new TreeNode(Integer.parseInt(s[index]));
                    queue.offer(curr.left);
                }
            }

            index++;
            if (index < s.length){
                if (s[index].equals("null")){
                    curr.right = null;
                }
                else{
                    curr.right = new TreeNode(Integer.parseInt(s[index]));
                    queue.offer(curr.right);
                }
            }
        }
        return root;

    }


}

```

### Idea

- DFS
  Just like post order traversal, the root will be add with left and right. In the deserializing process, queue can help maintain the order.

### Pseudocode

```
null

```

### Implementation

```
public class Codec {

    private static final String NULL_SYMBOL = "null";
    private static final String DELIMITER = ",";
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null){
            return NULL_SYMBOL + DELIMITER;
        }
        String left = serialize(root.left);
        String right = serialize(root.right);

        return root.val + DELIMITER + left + right;

    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Queue<String> nodesLeftToMaterialize = new LinkedList<>();
        nodesLeftToMaterialize.addAll(Arrays.asList(data.split(DELIMITER)));
        return helper(nodesLeftToMaterialize);
    }
    public TreeNode helper(Queue<String> nodes){
        String node = nodes.poll();
        if (node.equals("null")){
            return null;
        }
        TreeNode newNode = new TreeNode(Integer.valueOf(node));
        newNode.left = helper(nodes);
        newNode.right = helper(nodes);
        return newNode;
    }

}

```
