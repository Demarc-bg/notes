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
    class Validation{
        boolean v;
        Validation(){
            this.v = true;
        }
    }
    public boolean isValidBST(TreeNode root) {
        if(root==null) return true;
        ArrayList<Integer> value = new ArrayList<Integer>(1);
        Validation validation = new Validation();
        Solution.iterate(root,value,validation);
        return validation.v;
    }
    public static void iterate(TreeNode root, ArrayList<Integer> value, Validation validation){
        if(root.left!=null){
            Solution.iterate(root.left, value,validation);
        }
        if(value.isEmpty()) value.add(root.val);
        else {
            if(value.get(0)>=root.val) validation.v = false;
            else value.set(0,root.val);
        }
        if(root.right!=null){
            Solution.iterate(root.right, value,validation);
        }
    }
}
```

