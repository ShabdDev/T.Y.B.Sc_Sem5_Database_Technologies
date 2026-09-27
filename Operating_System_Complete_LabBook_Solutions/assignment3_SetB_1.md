# Assignment 3 — Set B — MFU Page Replacement

## Question (as given in the lab book)

i. Write the simulation program to implement demand paging and show the page scheduling and total number of page faults for the following given page reference string. Give input n as the number of memory frames.

Reference String: 2,5,2,8,5,4,1,2,3,2,6,1,2,5,9,8

1) Implement MFU
2) Implement Optimal

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#define MAX 100

int main(void) {
    int frames[MAX], freq[MAX], age[MAX], ref[MAX], n, m;
    int faults = 0, time = 0;

    printf("Enter number of frames: ");
    scanf("%d", &n);
    printf("Enter length of reference string: ");
    scanf("%d", &m);
    printf("Enter reference string: ");
    for (int i = 0; i < m; i++) scanf("%d", &ref[i]);

    for (int i = 0; i < n; i++) {
        frames[i] = -1; freq[i] = 0; age[i] = 0;
    }

    printf("\nPage\tFrames\t\tResult\n");
    for (int i = 0; i < m; i++) {
        time++;
        int pos = -1;
        for (int j = 0; j < n; j++)
            if (frames[j] == ref[i]) pos = j;

        int hit = (pos != -1);

        if (hit) {
            freq[pos]++;
        } else {
            int victim = -1;
            for (int j = 0; j < n; j++)
                if (frames[j] == -1) { victim = j; break; }

            if (victim == -1) {
                victim = 0;
                for (int j = 1; j < n; j++) {
                    if (freq[j] > freq[victim] ||
                       (freq[j] == freq[victim] && age[j] < age[victim]))
                        victim = j;
                }
            }

            frames[victim] = ref[i];
            freq[victim] = 1;
            age[victim] = time;
            faults++;
        }

        printf("%d\t", ref[i]);
        for (int j = 0; j < n; j++) printf("%2d ", frames[j]);
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



## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 32.
