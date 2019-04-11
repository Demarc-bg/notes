### 基于java的约瑟夫问题

```java
// using linkedList, time cost O(n^2)
// better than using array, avoid the index access problem.
public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNextInt()){
            int peopleNum = sc.nextInt();
            int jump = sc.nextInt();
            LinkedList<Integer> people = new LinkedList<>();
            for(int i=0;i<peopleNum;i++)
            	people.add(i+1);
            int index = 0;
            for(int i=0;i<peopleNum-1;i++) {
            	index = (index+jump-1)%people.size();
            	System.out.print(people.get(index));
            	if(i<peopleNum-2)System.out.print(" ");
            	people.remove(index);
            }
            System.out.println();
            System.out.println(people.getFirst());
        }
}
```

