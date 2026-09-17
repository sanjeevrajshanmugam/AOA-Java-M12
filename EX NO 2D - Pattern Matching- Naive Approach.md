
# EX 2D Pattern Matching using Naive Approach.
## DATE: 17.09.2026
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
