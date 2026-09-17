# EX 2A Assign Cookies using Greedy Algorithm. 
## DATE: 17.09.26
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


# EX 2B Jump Game using Greedy Algorithm.

## AIM:
To write a Java program to for given constraints.
You are given an array of integers. Each number represents the maximum number of steps you can jump forward from that position.

You start from the first element (index 0). 
Write a program to find the minimum number of jumps required to reach the last index of the array.

If it is not possible to reach the end, return -1.

## Algorithm:

1.Read the number of elements and store them in an array.

2.Handle base conditions:

  (i)If array length is 1 → 0 jumps.
  
  (ii)If the first element is 0 → cannot move → return -1.

3.Initialise jumps = 0, end = 0, and farthest = 0.

4.Traverse the array and at each index update the farthest reachable index.

5.When the current index reaches the end of the current jump range, increase jump count.

6.If at any point farthest reaches or crosses the last index, return the jump count.

7.Print the minimum jumps needed.

## Program:
```
/*
Program to implement Reverse a String
Developed by: SANJEEV RAJ S
Register Number: 212223220096
*/
import java.util.Scanner;

public class MinJumpToEnd {

    public static int minimumJumps(int[] array) {
        int n = array.length;
        if (n <= 1) return 0;
        if (array[0] == 0) return -1;

        int jumps = 0, end = 0, farthest = 0;

        for (int i = 0; i < n - 1; i++) {
            farthest = Math.max(farthest, i + array[i]);

            if (i == end) {
                jumps++;
                end = farthest;
                if (end >= n - 1) return jumps;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] nums = new int[n];

        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        System.out.println("Minimum jumps to reach last index: " + minimumJumps(nums));
    }
}
```

## Output:

<img width="1056" height="353" alt="517325753-d3dce493-e9dd-42de-8c52-53e2181933a8" src="https://github.com/user-attachments/assets/b560f488-9e9d-4a25-8bcd-f003f14946ef" />


## Result:
The program successfully implemented and the expected output is verified.


# EX 2C Job Sequencing using Greedy Approach

## AIM:
To write a Java program that schedules jobs using the Greedy Approach. Each job has:

A unique Job ID
A Deadline
A Profit (earned only if the job is completed on or before its deadline)
Each job takes 1 unit of time and only one job can be done at a time. The goal is to complete the maximum number of jobs with the maximum total profit.

## Algorithm:

1.Read the number of jobs and input each job’s id, deadline, and profit.

2.Sort the jobs in decreasing order of profit.

3.Find the maximum deadline among all jobs.

4.Create a time-slot array to track free and occupied slots.

5.For each job in sorted order, assign it to the latest free slot before or on its deadline.

6.Count how many jobs were done and compute the total profit.

7.Print the number of jobs completed and the total profit.

## Program:
```
/*
Program to implement Reverse a String
Developed by: SANJEEV RAJ S
Register Number: 212223220096
*/
import java.util.*;

public class JobScheduling {

    static class Job {
        int id, deadline, profit;

        Job(int id, int deadline, int profit) {
            this.id = id;
            this.deadline = deadline;
            this.profit = profit;
        }
    }

    public static int[] jobScheduling(Job[] jobs, int n) {
        Arrays.sort(jobs, (a, b) -> b.profit - a.profit);
        int maxDeadline = 0;

        for(Job job : jobs) {
            maxDeadline = Math.max(maxDeadline, job.deadline);
        }

        boolean[] slot = new boolean[maxDeadline + 1];
        int jobsDone = 0, totalProfit = 0;

        for(Job job : jobs) {
            for(int j = job.deadline; j > 0; j--) {
                if(!slot[j]) {
                    slot[j] = true;
                    jobsDone++;
                    totalProfit += job.profit;
                    break;
                }
            }
        }
        return new int[]{jobsDone, totalProfit};
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Job[] jobs = new Job[n];

        for(int i = 0; i < n; i++) {
            int id = sc.nextInt();
            int deadline = sc.nextInt();
            int profit = sc.nextInt();
            jobs[i] = new Job(id, deadline, profit);
        }

        int[] result = jobScheduling(jobs, n);
        System.out.println(result[0] + " " + result[1]);
    }
}
```

## Output:

<img width="1088" height="452" alt="516748585-5144a831-ee44-4454-868b-ea0a42ace496" src="https://github.com/user-attachments/assets/7a5b7a85-fcea-4158-aeeb-dc7201865d8f" />


## Result:
The program successfully implemented and the expected output is verified.


# EX 2D Pattern Matching using Naive Approach.

## AIM:
To write a Java program to for given constraints.
Given text string with length n and a pattern with length m, the task is to prints all occurrences of pattern in text.
Note: You may assume that n > m.

Examples: 

Input:  text = "THIS IS A TEST TEXT", pattern = "TEST"
Output: Pattern found at index 10

Input:  text =  "AABAACAADAABAABA", pattern = "AABA"
Output: Pattern found at index 0, Pattern found at index 9, Pattern found at index 12

## Algorithm:

1.Read the text string and the pattern string.

2.Find the lengths of the text (n) and pattern (m).

3.Loop from index 0 to n - m.

4.For each position, compare characters of text and pattern one by one.

5.If all characters match, print the index where the pattern starts.

## Program:
```
/*
Program to implement Reverse a String
Developed by: SANJEEV RAJ S
Register Number: 212223220096 
*/
import java.util.Scanner;

public class NaivePatternSearch {

    static void search(String text, String pattern){
        int n = text.length();
        int m = pattern.length();

        for(int i = 0; i <= n - m; i++){
            int j;
            for(j = 0; j < m; j++){
                if(text.charAt(i + j) != pattern.charAt(j)){
                    break;
                }
            }
            if(j == m){
                System.out.println("Pattern found at index " + i);
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        String text = scanner.nextLine();
        String pattern = scanner.nextLine();

        search(text, pattern);

        scanner.close();
    }
}
```

## Output:

<img width="1183" height="304" alt="517206941-c4a3cdcc-80fb-43b0-a41e-1050bc74351c" src="https://github.com/user-attachments/assets/c6ec17b9-ec75-4ce1-8180-fcfffde3bdeb" />


## Result:
The program successfully implemented and the expected output is verified.


# EX 2E Pattern Matching using KMP Algorithm.

## AIM:
To write a Java program for the following constraints.
Longest Palindromic Substring
Given a string s, return the longest palindromic substring in s.
using Manacher's Algorithm

## Algorithm:
1.Convert the input string by inserting # between characters to handle even-length palindromes.

2.Maintain an array P[] to store the radius (half-length) of palindromes around each centre.

3.Use two variables:

C → current center

R → right boundary of the current palindrome

4.For every character:

Mirror the index across the centre and update value of P[i]

Expand around the centre to update palindrome radius

If the palindrome goes beyond R, update C and R

5.Find the maximum radius in P[] and extract the longest palindromic substring from the original string.

## Program:
```
/*
Program to implement Reverse a String
Developed by: SANJEEV RAJ S
Register Number: 212223220096
*/

import java.util.Scanner;

public class Manacher {

    public static String longestPalindrome(String s) {
        if (s == null || s.length() == 0) return "";

        String t = preprocess(s);
        int n = t.length();
        int[] P = new int[n];

        int C = 0;
        int R = 0;

        for (int i = 1; i < n - 1; i++) {
            int mirror = 2 * C - i;

            if (i < R)
                P[i] = Math.min(R - i, P[mirror]);

            while (t.charAt(i + (1 + P[i])) == t.charAt(i - (1 + P[i]))) {
                P[i]++;
            }

            if (i + P[i] > R) {
                C = i;
                R = i + P[i];
            }
        }

        int maxLen = 0;
        int centerIndex = 0;
        for (int i = 1; i < n - 1; i++) {
            if (P[i] > maxLen) {
                maxLen = P[i];
                centerIndex = i;
            }
        }

        int start = (centerIndex - maxLen) / 2;
        return s.substring(start, start + maxLen);
    }

    private static String preprocess(String s) {
        StringBuilder sb = new StringBuilder();
        sb.append("^");
        for (char c : s.toCharArray()) {
            sb.append("#").append(c);
        }
        sb.append("#$");
        return sb.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = scanner.nextLine();

        String result = longestPalindrome(input);
        System.out.println("Longest Palindromic Substring: " + result);

        scanner.close();
    }
}
```

## Output:

<img width="1213" height="259" alt="517208277-49175af7-a47c-4db1-a64a-c646ecaec7e6" src="https://github.com/user-attachments/assets/2b3116a5-7a63-40e3-bd5c-b012f720995d" />


## Result:
The program successfully implemented and the expected output is verified.
