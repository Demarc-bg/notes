### BackTracking22. Generate Parentheses

```
For example, given n = 3, a solution set is:
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]

```

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList(2*n);
        Solution.backTracking(result,new StringBuilder(),n,n);
        return result;
    }
    //actually don't need isValid()
    public static boolean isValid(String testString){
        //if(cacheString.length()==0) return true;
        //String testString = cacheString.toString();
        //LinkedList can be faster.
        LinkedList<Character> link = new LinkedList<Character>();
        for(int i=0;i<testString.length();i++){
            if(testString.charAt(i)=='(') link.add('(');
            else {
                if(link.isEmpty()) return false;
                link.remove(link.size()-1);
            }
        }
        return true;
    }
    public static void backTracking
        (List<String> result, StringBuilder cacheString,int left, int right){
        if(left==0&&right==0){
            String insertStr = cacheString.toString();
            // if(!result.contains(insertStr)&&Solution.isValid(insertStr))
            // if(Solution.isValid(insertStr))
                result.add(insertStr);
        }
        else{
            if(left>0){
                cacheString.append('(');
                Solution.backTracking(result,cacheString,left-1,right);
                cacheString.deleteCharAt(cacheString.length()-1);
            }
            //rule: right must bigger than left.
            if(right>0&&right>left){
                cacheString.append(')');
                Solution.backTracking(result,cacheString,left,right-1);
                cacheString.deleteCharAt(cacheString.length()-1);
            }
        }
    }
}
```

