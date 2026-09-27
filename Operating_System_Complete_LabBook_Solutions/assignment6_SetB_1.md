# Assignment 6 — Set B — SCAN Disk Scheduling

## Question (as given in the lab book)

i. Write an OS program to implement SCAN Disk Scheduling algorithm.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <stdlib.h>

void sort(int a[],int n){
    for(int i=0;i<n-1;i++)for(int j=i+1;j<n;j++)
        if(a[i]>a[j]){int t=a[i];a[i]=a[j];a[j]=t;}
}

int main(void){
    int n,head,size,dir,req[100],total=0;
    printf("Enter disk size (number of cylinders): ");scanf("%d",&size);
    printf("Enter number of requests: ");scanf("%d",&n);
    printf("Enter request sequence: ");for(int i=0;i<n;i++)scanf("%d",&req[i]);
    printf("Enter initial head position: ");scanf("%d",&head);
    printf("Direction (0 = left, 1 = right): ");scanf("%d",&dir);

    sort(req,n);
    printf("\nService order: %d",head);

    if(dir==1){
        for(int i=0;i<n;i++)if(req[i]>=head){
            total+=abs(head-req[i]);head=req[i];printf(" -> %d",head);
        }
        if(head!=size-1){total+=abs(head-(size-1));head=size-1;printf(" -> %d",head);}
        for(int i=n-1;i>=0;i--)if(req[i]<head){
            total+=abs(head-req[i]);head=req[i];printf(" -> %d",head);
        }
    }else{
        for(int i=n-1;i>=0;i--)if(req[i]<=head){
            total+=abs(head-req[i]);head=req[i];printf(" -> %d",head);
        }
        if(head!=0){total+=head;head=0;printf(" -> 0");}
        for(int i=0;i<n;i++)if(req[i]>head){
            total+=abs(head-req[i]);head=req[i];printf(" -> %d",head);
        }
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

Enter disk size, request sequence, initial head and direction. `0` means left and `1` means right. SCAN moves to the physical end of the disk before reversing.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 51.
