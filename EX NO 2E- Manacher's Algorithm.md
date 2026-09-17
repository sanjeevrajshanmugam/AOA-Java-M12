
# EX 2E Pattern Matching using KMP Algorithm.
## DATE: 17.09.26
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
