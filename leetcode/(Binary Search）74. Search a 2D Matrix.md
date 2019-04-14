### (Binary Search）74. Search a 2D Matrix

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix==null||matrix.length == 0||matrix[0].length == 0) return false;
        int left = 0, right = matrix.length-1;
        int mid = (left+right)/2;
        while(left+1<right){
            if(matrix[mid][0]>target) right = mid - 1;
            else left = mid;
            mid = (left+right)/2;
        }
        return searchLine(target>=matrix[right][0]?matrix[right]:matrix[left],target);
        
    }
    public boolean searchLine(int[] matrix , int target){
        int left = 0, right = matrix.length-1;
        int mid = (left+right)/2;
        while(left<right){
            if(matrix[mid] == target) return true;
            if(matrix[mid] > target) right = mid-1;
            else left = mid +1;
            mid = (left+right)/2;
        }
        return matrix[mid] == target?true:false;
        
    }
}
```

