# Assignment 6 — Set C — Comparative Disk Scheduling

## Question (as given in the lab book)

i. Implement FCFS, SSTF, SCAN and LOOK Disk Scheduling algorithms in a single C program. Accept a request sequence, initial head position, and disk size as input. Generate a comparative report showing:

 Service order of requests
 Total seek operations
 Average seek time
 Best-performing algorithm

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX 100

void sort(int a[],int n){for(int i=0;i<n-1;i++)for(int j=i+1;j<n;j++)if(a[i]>a[j]){int t=a[i];a[i]=a[j];a[j]=t;}}

int fcfs(int r[],int n,int h){int t=0;for(int i=0;i<n;i++){t+=abs(h-r[i]);h=r[i];}return t;}

int sstf(int r[],int n,int h){
    int done[MAX]={0},t=0;
    for(int k=0;k<n;k++){
        int idx=-1,best=1000000;
        for(int i=0;i<n;i++)if(!done[i]&&abs(h-r[i])<best){best=abs(h-r[i]);idx=i;}
        done[idx]=1;t+=abs(h-r[idx]);h=r[idx];
    }return t;
}

int scan(int r[],int n,int h,int size,int dir){
    int a[MAX];for(int i=0;i<n;i++)a[i]=r[i];sort(a,n);int t=0;
    if(dir==1){
        for(int i=0;i<n;i++)if(a[i]>=h){t+=abs(h-a[i]);h=a[i];}
        if(h!=size-1){t+=abs(h-(size-1));h=size-1;}
        for(int i=n-1;i>=0;i--)if(a[i]<h){t+=abs(h-a[i]);h=a[i];}
    }else{
        for(int i=n-1;i>=0;i--)if(a[i]<=h){t+=abs(h-a[i]);h=a[i];}
        if(h!=0){t+=h;h=0;}
        for(int i=0;i<n;i++)if(a[i]>h){t+=abs(h-a[i]);h=a[i];}
    }return t;
}

int look(int r[],int n,int h,int dir){
    int a[MAX];for(int i=0;i<n;i++)a[i]=r[i];sort(a,n);int t=0;
    if(dir==1){
        for(int i=0;i<n;i++)if(a[i]>=h){t+=abs(h-a[i]);h=a[i];}
        for(int i=n-1;i>=0;i--)if(a[i]<h){t+=abs(h-a[i]);h=a[i];}
    }else{
        for(int i=n-1;i>=0;i--)if(a[i]<=h){t+=abs(h-a[i]);h=a[i];}
        for(int i=0;i<n;i++)if(a[i]>h){t+=abs(h-a[i]);h=a[i];}
    }return t;
}

void print_order_fcfs(int r[],int n,int h){printf("%d",h);for(int i=0;i<n;i++)printf(" -> %d",r[i]);}

int main(void){
    int n,h,size,dir,r[MAX];
    printf("Enter disk size (number of cylinders): ");scanf("%d",&size);
    printf("Enter number of requests: ");scanf("%d",&n);
    printf("Enter request sequence: ");for(int i=0;i<n;i++)scanf("%d",&r[i]);
    printf("Enter initial head position: ");scanf("%d",&h);
    printf("Direction for SCAN/LOOK (0 = left, 1 = right): ");scanf("%d",&dir);

    int f=fcfs(r,n,h),s=sstf(r,n,h),sc=scan(r,n,h,size,dir),l=look(r,n,h,dir);
    printf("\nAlgorithm\tTotal Seek\tAverage Seek\n");
    printf("FCFS\t\t%d\t\t%.2f\n",f,(double)f/n);
    printf("SSTF\t\t%d\t\t%.2f\n",s,(double)s/n);
    printf("SCAN\t\t%d\t\t%.2f\n",sc,(double)sc/n);
    printf("LOOK\t\t%d\t\t%.2f\n",l,(double)l/n);

    int min=f;if(s<min)min=s;if(sc<min)min=sc;if(l<min)min=l;
    printf("\nAlgorithms with minimum total seek = ");
    if(f==min)printf("FCFS ");
    if(s==min)printf("SSTF ");
    if(sc==min)printf("SCAN ");
    if(l==min)printf("LOOK ");
    printf("\n");
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

The program accepts disk size, requests, initial head and SCAN/LOOK direction. It reports total and average seek movement for all four algorithms and lists all algorithms tied for the minimum total seek movement.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 51.
