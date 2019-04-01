### InOrder94. Binary Tree Inorder Traversal

Two ways: recursion and iterations.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
// recursive solution
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if(root==null) return result;
        Solution.Inorder(root,result);
        return result;
    }
    public static void Inorder(TreeNode root, List<Integer> result){
        if(root.left!=null){
            Solution.Inorder(root.left,result);
        }
        result.add(root.val);
        if(root.right!=null){
            Solution.Inorder(root.right,result);
        }
    }
}
```

```

```

