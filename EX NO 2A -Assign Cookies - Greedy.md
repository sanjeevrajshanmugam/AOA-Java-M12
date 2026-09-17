# EX 2A Assign Cookies using Greedy Algorithm. 
## DATE: 17.08.26
## AIM:
To Write a Java program for the following Constraints.
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximise the number of your content children and output the maximum number.

## Algorithm:

1.Read the number of children and their greed values.

2.Read the number of cookies and their sizes.

3.Sort both arrays in ascending order.

4.Use two pointers to match the smallest available cookie to the least greedy child.

5.Count each successful assignment and print the total. 

## Program:
```
/*
Program to implement Reverse a String
Developed by: SANJEEV RAJ S
Register Number: 212223220096
*/
import java.util.*;

public class AssignCookies {
    
    public static int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int i = 0, j = 0;

        while(i < g.length && j < s.length){
            if(s[j] >= g[i]) i++;
            j++;
        }
        return i;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] g = new int[n];
        for (int i = 0; i < n; i++) g[i] = sc.nextInt();

        int m = sc.nextInt();
        int[] s = new int[m];
        for (int i = 0; i < m; i++) s[i] = sc.nextInt();

        System.out.println(findContentChildren(g, s));
    }
}
```

## Output:

<img width="1031" height="402" alt="516742204-7d30fdae-b8a4-4b5e-9de6-f28dded1bfae" src="https://github.com/user-attachments/assets/580649fa-a4a7-4ff9-b3ff-a2b1dd146c35" />


## Result:
The program successfully print all the numbers from 1 to N. 
