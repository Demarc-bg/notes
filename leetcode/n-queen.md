```java
public List<List<String>> solveNQueens(int n) {
	        String[] dic = new String[n];
	        for(int i=0;i<n;i++){
	            StringBuilder cache = new StringBuilder(8);
	            for(int j=0;j<n;j++){
	                if(i==j) cache.append('Q');
	                else cache.append('.');
	            }
	            dic[i] = cache.toString();
	        }
	        List<List<String>> result = new ArrayList<List<String>>(n*2);
	        Solution.backTracking(result,new ArrayList<String>(8),dic,0,0,n);
	        return result;
	    }
	    public static void backTracking
	        (List<List<String>> result, List<String> cacheList, String[] dic,int level, int nextPos,int n){
	        if(level == n){
	            result.add(cacheList);
	        }
	        else {
	            for(int i = nextPos;i<n;i++){
	                String singleRow = dic[i];
	                if(!cacheList.contains(singleRow))cacheList.add(singleRow);
	                else return;
	                Solution.backTracking(result,cacheList,dic,level+1,(i+2)%n,n);
	                cacheList.remove(cacheList.size()-1);
	            }
	        }
	    }	
```

