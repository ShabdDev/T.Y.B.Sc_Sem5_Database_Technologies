# Assignment 4 — Set C — Resource Request Algorithm

## Question (as given in the lab book)

I) Consider a system with ‘n’ processes and ‘m’ resource types. Accept number of instances for every resource type. For each process accept the allocation and maximum requirement matrices. Write a program to display the contents of need matrix and to check if the given request of a process can be granted immediately or not. By using resource request Algorithm

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#define MAX 10

int safety(int n,int m,int alloc[MAX][MAX],int need[MAX][MAX],
           int available[MAX],int sequence[MAX]){
    int work[MAX],finish[MAX]={0},count=0;
    for(int j=0;j<m;j++)work[j]=available[j];

    while(count<n){
        int found=0;
        for(int i=0;i<n;i++){
            if(finish[i])continue;
            int ok=1;
            for(int j=0;j<m;j++)if(need[i][j]>work[j])ok=0;
            if(ok){
                for(int j=0;j<m;j++)work[j]+=alloc[i][j];
                finish[i]=1; sequence[count++]=i; found=1;
            }
        }
        if(!found)break;
    }
    return count==n;
}

int main(void){
    int n,m,total[MAX],available[MAX],alloc[MAX][MAX],max[MAX][MAX],need[MAX][MAX];

    printf("Enter number of processes and resource types: ");
    scanf("%d%d",&n,&m);

    printf("Enter total instances of each resource type:\n");
    for(int j=0;j<m;j++)scanf("%d",&total[j]);

    printf("Enter Allocation matrix:\n");
    for(int i=0;i<n;i++)for(int j=0;j<m;j++)scanf("%d",&alloc[i][j]);

    printf("Enter Max matrix:\n");
    for(int i=0;i<n;i++)for(int j=0;j<m;j++)scanf("%d",&max[i][j]);

    for(int j=0;j<m;j++){
        int used=0;
        for(int i=0;i<n;i++)used+=alloc[i][j];
        available[j]=total[j]-used;
    }

    for(int i=0;i<n;i++)for(int j=0;j<m;j++)need[i][j]=max[i][j]-alloc[i][j];

    printf("\nNeed Matrix\n");
    for(int i=0;i<n;i++){for(int j=0;j<m;j++)printf("%d ",need[i][j]);printf("\n");}

    int p,request[MAX];
    printf("\nEnter process number making request (0-%d): ",n-1);
    scanf("%d",&p);
    printf("Enter request vector: ");
    for(int j=0;j<m;j++)scanf("%d",&request[j]);

    for(int j=0;j<m;j++){
        if(request[j]>need[p][j]){
            printf("Request cannot be granted: it exceeds the process's remaining Need.\n");
            return 0;
        }
        if(request[j]>available[j]){
            printf("Request cannot be granted immediately: resources are not Available.\n");
            return 0;
        }
    }

    /* Tentative allocation */
    for(int j=0;j<m;j++){
        available[j]-=request[j];
        alloc[p][j]+=request[j];
        need[p][j]-=request[j];
    }

    int sequence[MAX];
    if(safety(n,m,alloc,need,available,sequence)){
        printf("\nRequest CAN be granted immediately.\n");
        printf("Safe sequence after tentative allocation: ");
        for(int i=0;i<n;i++)printf("P%d%s",sequence[i],i==n-1?"\n":" -> ");
    }else{
        printf("\nRequest CANNOT be granted because it would make the system unsafe.\n");
        printf("The tentative allocation must be rolled back.\n");
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

The program derives Available from total resource instances minus current Allocation, checks `Request <= Need` and `Request <= Available`, tentatively allocates the request, and then runs the Safety Algorithm. If the resulting state is unsafe, the request is rejected.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 41.
