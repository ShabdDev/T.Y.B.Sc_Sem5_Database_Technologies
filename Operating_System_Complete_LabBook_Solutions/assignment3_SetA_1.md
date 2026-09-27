# Assignment 3 — Set A — FIFO Page Replacement

## Question (as given in the lab book)

i. Write the simulation program to implement demand paging and show the page scheduling and total number of page faults for the following given page reference string. Give input n as the number of memory frames.

Reference String: 12,15,12,18,6,8,11,12,19,12,6,8,12,15,19,8

1) Implement FIFO

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#define MAX 100

int main(void) {
    int frames[MAX], ref[MAX], n, m, faults = 0, pointer = 0;
    printf("Enter number of frames: ");
    scanf("%d", &n);
    printf("Enter length of reference string: ");
    scanf("%d", &m);
    printf("Enter reference string: ");
    for (int i = 0; i < m; i++) scanf("%d", &ref[i]);

    for (int i = 0; i < n; i++) frames[i] = -1;

    printf("\nPage\tFrames\t\tResult\n");
    for (int i = 0; i < m; i++) {
        int hit = 0;
        for (int j = 0; j < n; j++)
            if (frames[j] == ref[i]) hit = 1;

        if (!hit) {
            frames[pointer] = ref[i];
            pointer = (pointer + 1) % n;
            faults++;
        }

        printf("%d\t", ref[i]);
        for (int j = 0; j < n; j++)
            printf("%2d ", frames[j]);
        printf("\t%s\n", hit ? "Hit" : "Page Fault");
    }

    printf("\nTotal page faults = %d\n", faults);
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

For the exact workbook reference string, enter its 16 values when prompted. The number of frames `n` is supplied by you.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 31.
