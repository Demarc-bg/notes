### (Binary Search)33. Search in Rotated Sorted Array

**double binary Search**

```java
class Solution {
    public int search(int[] nums, int target) {
        if(nums.length == 0) return -1;
        return rotatedIndex(nums,target);
    }
    public static int rotatedIndex(int[] nums, int target){
        int left = 0, right = nums.length-1;
        int mid = (left+right)/2;
        // if contains rotated list
        if(nums[0]>nums[nums.length-1]){
            // the crossing two indeices including the rotatedIndex
            while(left+1<right){
                if(nums[mid]>nums[left]){
                    left = mid;
                }
                else right = mid;
                mid = (left+right)/2;
            }
            // to indentify rotatedList
            left = right;
        }
        if(target>=nums[0])
            // Veryify whether left==right to input correct parameters
            return binarySearch(nums,0,left==right?right-1:right,target);
        else if(target<=nums[nums.length-1])    
            return binarySearch(nums,right,nums.length-1,target);
        else return -1;
    }
    public static int binarySearch(int[] nums, int left, int right, int target){
        int mid = (left+right)/2;
        while(left<right){
            if(nums[mid]==target) return mid;
            else if(nums[mid]<target) left = mid+1;
            else right = mid-1;
            mid = (left+right)/2;
        }
        return nums[mid]==target?mid:-1;
    }
}
```

