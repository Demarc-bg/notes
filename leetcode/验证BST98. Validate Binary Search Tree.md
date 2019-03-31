### 98. Validate Binary Search Tree

To validate a binary search tree, use inOrder searching is a good choice.

```
Input:
    2
   / \
  1   3
Output: true
```



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
class Solution {
    public boolean isValidBST(TreeNode root) {
        List<Integer> value = new ArrayList<Integer>();
        if(root==null) return true;
        Solution.iterate(root,value);
        int size = value.size();
        for(int i=0;i<size-1;i++){
            if(value.get(i)>=value.get(i+1)) return false;
        }
        return true;
    }
    public static void iterate(TreeNode root, List value){
        if(root == null) return;
        if(root.left!=null){
            Solution.iterate(root.left, value);
            //value.add(root.left.val;)
        }
        value.add(root.val);
        if(root.right!=null){
            Solution.iterate(root.right, value);
            //value.add(root.right.val);
        }
    }
}
```

