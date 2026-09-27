# Assignment 6 — Set A — FCFS Disk Scheduling

## Question (as given in the lab book)

i. Write an OS program to implement FCFS Disk Scheduling algorithm.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <stdlib.h>

int main(void){
    int n,head,req[100],total=0;
    printf("Enter number of requests: ");scanf("%d",&n);
    printf("Enter request sequence: ");for(int i=0;i<n;i++)scanf("%d",&req[i]);
    printf("Enter initial head position: ");scanf("%d",&head);

    printf("\nService order: %d",head);
    for(int i=0;i<n;i++){
        total += abs(head-req[i]);
        head=req[i];
        printf(" -> %d",head);
    }
    printf("\nTotal head movement = %d cylinders\n",total);
    printf("Average seek movement = %.2f cylinders/request\n",(double)total/n);
    return 0;
}
```

## Compile

```bash
gcc -std=c11 -Wall -Wextra program.c -o program
```

## Run

```bash
./program
```

Enter the request sequence and initial head position. The program prints the service order, total head movement and average seek movement.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 51.
