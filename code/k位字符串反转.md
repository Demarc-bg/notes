### k位字符串反转

```
first row is the linkedList
second row is the k reverse length
input:
[1,2,3,42,51]
2
output:
[2,1,42,3,51]
```

```java
public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		while (in.hasNext()) {
			String str = in.next();
			int k = in.nextInt();
			if (k <= 1 || str.length() - 1 == 2 * k || str.length() <= 4) {
				System.out.println(str);
			} else {
				System.out.print("[");
                // split by ","
				String[] input = str.substring(1, str.length() - 1).split(",");
				for (int i = 0; i < input.length;) {
					if (i + k - 1 <= input.length - 1) {
						for (int j = i + k - 1; j >= i; j--) {
							System.out.print(input[j]);
                            // special for the case that input.length can divide by k
							if (i + (k - 1) != input.length - 1 || j != i)
								System.out.print(",");
						}
						i += k;
					} else {
						System.out.print(input[i]);
						if (i != input.length - 1)
							System.out.print(",");
						i++;
					}
				}
				System.out.print("]");
			}
		}
	}
public static boolean isLowCase(char c){
        if(c>='a'&&c<='z') return true;
        else return false;
    }
```

