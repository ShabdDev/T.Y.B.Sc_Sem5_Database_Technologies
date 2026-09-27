# Assignment 4 — Set B — Safety Algorithm

## Question (as given in the lab book)

I) Modify above program so as to include the following:
a) Accept Available and Display Available Matrix and Implement Safety Algorithm

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#define MAX 10

int main(void) {
    int n,m,alloc[MAX][MAX],max[MAX][MAX],need[MAX][MAX];
    int available[MAX],work[MAX],finish[MAX]={0},safe[MAX],count=0;

    printf("Enter number of processes and resource types: ");
    scanf("%d%d",&n,&m);

    printf("Enter Allocation matrix:\n");
    for(int i=0;i<n;i++)for(int j=0;j<m;j++)scanf("%d",&alloc[i][j]);

    printf("Enter Max matrix:\n");
    for(int i=0;i<n;i++)for(int j=0;j<m;j++)scanf("%d",&max[i][j]);

    printf("Enter Available vector:\n");
    for(int j=0;j<m;j++){scanf("%d",&available[j]);work[j]=available[j];}

    for(int i=0;i<n;i++)for(int j=0;j<m;j++)need[i][j]=max[i][j]-alloc[i][j];

    printf("\nNeed Matrix\n");
    for(int i=0;i<n;i++){for(int j=0;j<m;j++)printf("%d ",need[i][j]);printf("\n");}

    while(count<n){
        int found=0;
        for(int i=0;i<n;i++){
            if(finish[i])continue;
            int possible=1;
            for(int j=0;j<m;j++)
                if(need[i][j]>work[j])possible=0;

            if(possible){
                for(int j=0;j<m;j++)work[j]+=alloc[i][j];
                finish[i]=1;
                safe[count++]=i;
                found=1;
            }
        }
        if(!found)break;
    }

    if(count==n){
        printf("\nSystem is in SAFE state.\nSafe sequence: ");
        for(int i=0;i<n;i++)printf("P%d%s",safe[i],i==n-1?"\n":" -> ");
    }else{
        printf("\nSystem is NOT in a safe state.\n");
    }
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

The program additionally accepts the Available vector and executes the Banker's Safety Algorithm to find a safe sequence.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 41.
