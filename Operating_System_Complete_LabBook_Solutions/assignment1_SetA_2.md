# Assignment 1 — Set A — Question 2: fork(), Bubble Sort and Insertion Sort

## Question (as given in the lab book)

(2) Implement the C program to accept n integers to be sorted. Main function creates child process using fork system call. Parent process sorts the integers using bubble sort and waits for child process using wait system call. Child process sorts the integers using insertion sort.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

void bubbleSort(int a[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - i - 1; j++)
            if (a[j] > a[j + 1]) {
                int t = a[j]; a[j] = a[j + 1]; a[j + 1] = t;
            }
}

void insertionSort(int a[], int n) {
    for (int i = 1; i < n; i++) {
        int key = a[i], j = i - 1;
        while (j >= 0 && a[j] > key) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = key;
    }
}

void printArray(const char *label, int a[], int n) {
    printf("%s", label);
    for (int i = 0; i < n; i++) printf("%d ", a[i]);
    printf("\n");
}

int main(void) {
    int n;
    printf("Enter number of integers: ");
    scanf("%d", &n);

    int *a = malloc(n * sizeof(int));
    if (!a) return 1;

    printf("Enter %d integers: ", n);
    for (int i = 0; i < n; i++) scanf("%d", &a[i]);

    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        free(a);
        return 1;
    }

    if (pid == 0) {
        insertionSort(a, n);
        printArray("Child: insertion sort = ", a, n);
        free(a);
        return 0;
    }

    bubbleSort(a, n);
    printArray("Parent: bubble sort    = ", a, n);
    wait(NULL);
    printf("Parent: child process completed.\n");

    free(a);
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



## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 15.
