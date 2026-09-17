
# EX 2C Job Sequencing using Greedy Approach
## DATE: 17-09-26
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
