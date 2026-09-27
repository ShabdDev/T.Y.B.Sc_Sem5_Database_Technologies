# Assignment 5 — Set C — Indexed File Allocation

## Question (as given in the lab book)

Write a program to simulate Indexed file allocation method. Assume disk with n number of blocks. Give value of n as input. Write menu driven program with menu options as mentioned above and implement each option.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#define MAX 200
#define MAXFILES 50

typedef struct {
    char name[50];
    int indexBlock, length;
    int blocks[MAX];
} File;

int main(void){
    int n,bit[MAX],choice,count=0;
    File dir[MAXFILES];
    srand((unsigned)time(NULL));

    printf("Enter number of disk blocks: ");scanf("%d",&n);
    if(n<=1||n>MAX)return 1;
    for(int i=0;i<n;i++)bit[i]=rand()%2;

    while(1){
        printf("\n1. Show Bit Vector\n2. Create New File\n3. Show Directory\n4. Delete File\n5. Exit\n");
        printf("Enter choice: ");scanf("%d",&choice);

        if(choice==1){
            for(int i=0;i<n;i++)printf("%d",bit[i]);
            printf("\n(1 = free, 0 = allocated)\n");
        }else if(choice==2){
            char name[50];int blocks;
            printf("Enter file name and number of data blocks: ");scanf("%49s%d",name,&blocks);
            if(blocks<=0||blocks>=n||count>=MAXFILES){printf("Invalid request.\n");continue;}

            int freeCount=0;
            for(int i=0;i<n;i++)if(bit[i])freeCount++;
            if(freeCount<blocks+1){printf("Need %d free blocks: 1 index + %d data.\n",blocks+1,blocks);continue;}

            int index=-1,k=0;
            for(int i=0;i<n;i++)if(bit[i]){index=i;break;}
            bit[index]=0;

            for(int i=0;i<n&&k<blocks;i++){
                if(bit[i]){bit[i]=0;dir[count].blocks[k++]=i;}
            }

            strcpy(dir[count].name,name);
            dir[count].indexBlock=index;
            dir[count].length=blocks;
            count++;

            printf("File created. Index block = %d\nData blocks: ",index);
            for(int i=0;i<blocks;i++)printf("%d ",dir[count-1].blocks[i]);
            printf("\n");
        }else if(choice==3){
            printf("\nFile\tIndex\tData blocks\n");
            for(int i=0;i<count;i++){
                printf("%s\t%d\t",dir[i].name,dir[i].indexBlock);
                for(int j=0;j<dir[i].length;j++)printf("%d ",dir[i].blocks[j]);
                printf("\n");
            }
        }else if(choice==4){
            char name[50];printf("Enter file name: ");scanf("%49s",name);
            int idx=-1;
            for(int i=0;i<count;i++)if(strcmp(dir[i].name,name)==0){idx=i;break;}
            if(idx==-1){printf("File not found.\n");continue;}
            bit[dir[idx].indexBlock]=1;
            for(int j=0;j<dir[idx].length;j++)bit[dir[idx].blocks[j]]=1;
            for(int i=idx;i<count-1;i++)dir[i]=dir[i+1];
            count--;printf("File deleted; index and data blocks released.\n");
        }else if(choice==5)break;
        else printf("Invalid choice.\n");
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

The workbook's menu is:
1. Show Bit Vector
2. Create New File
3. Show Directory
4. Delete File
5. Exit

The bit vector is initialized randomly. In these implementations `1` means a free block and `0` means an allocated block, matching the workbook's example.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 45.
