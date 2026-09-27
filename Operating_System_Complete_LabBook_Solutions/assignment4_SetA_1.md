# Assignment 4 — Set A — Need Matrix

## Question (as given in the lab book)

I) Add the following functionalities in your program
a) Accept process and Resources
b) Display Allocation, Max
c) Display the contents of need matrix

Process Allocation MAX 
 A B C A B C 
P0 0 1 0 7 5 3 
P1 2 0 0 3 2 2 
P2 3 0 2 9 0 2 
P3 2 1 1 2 2 2 
P4 0 0 2 4 3 3

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#define MAX 10

int main(void) {
    int n, m, alloc[MAX][MAX], max[MAX][MAX], need[MAX][MAX];

    printf("Enter number of processes and resource types: ");
    scanf("%d%d", &n, &m);

    printf("Enter Allocation matrix:\n");
    for (int i=0;i<n;i++)
        for (int j=0;j<m;j++) scanf("%d",&alloc[i][j]);

    printf("Enter Max matrix:\n");
    for (int i=0;i<n;i++)
        for (int j=0;j<m;j++) scanf("%d",&max[i][j]);

    for (int i=0;i<n;i++)
        for (int j=0;j<m;j++)
            need[i][j]=max[i][j]-alloc[i][j];

    printf("\nAllocation Matrix\n");
    for (int i=0;i<n;i++){for(int j=0;j<m;j++)printf("%d ",alloc[i][j]);printf("\n");}

    printf("\nMax Matrix\n");
    for (int i=0;i<n;i++){for(int j=0;j<m;j++)printf("%d ",max[i][j]);printf("\n");}

    printf("\nNeed Matrix (Max - Allocation)\n");
    for (int i=0;i<n;i++){for(int j=0;j<m;j++)printf("%d ",need[i][j]);printf("\n");}

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

The program accepts `n`, `m`, Allocation and Max matrices and computes `Need = Max - Allocation`.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 40.
