# Assignment 1 — Set B — Question 2: execve() and Binary Search

## Question (as given in the lab book)

(2) Implement the C program that accepts an integer array. Main function forks child process. Parent process sorts an integer array and passes the sorted array to child process through the command line arguments of execve() system call. The child process uses execve() system call to load new program that uses this sorted array for performing the binary search to search the particular item in the array.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.

### Second source file: `binary_search.c`

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    if (argc < 3) {
        fprintf(stderr, "Usage: binary_search n target sorted_values...\n");
        return 1;
    }

    int n = atoi(argv[1]);
    int target = atoi(argv[2]);

    int low = 0, high = n - 1, pos = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        int value = atoi(argv[3 + mid]);

        if (value == target) {
            pos = mid;
            break;
        } else if (value < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    printf("Sorted array: ");
    for (int i = 0; i < n; i++) printf("%s ", argv[3 + i]);
    printf("\n");

    if (pos >= 0)
        printf("%d found at sorted index %d.\n", target, pos);
    else
        printf("%d not found.\n", target);

    return 0;
}
```

### Program

```c
#define _GNU_SOURCE
/* b2_parent.c
   Parent sorts the array and sends it through a pipe.
   Child builds argv[] and calls execve("./binary_search", ...).
*/
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <string.h>

extern char **environ;

void sort(int a[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if (a[i] > a[j]) {
                int t = a[i]; a[i] = a[j]; a[j] = t;
            }
}

int main(void) {
    int n, target;
    printf("Enter number of integers: ");
    scanf("%d", &n);

    int *a = malloc(n * sizeof(int));
    printf("Enter %d integers: ", n);
    for (int i = 0; i < n; i++) scanf("%d", &a[i]);

    printf("Enter item to search: ");
    scanf("%d", &target);

    int fd[2];
    if (pipe(fd) == -1) { perror("pipe"); return 1; }

    pid_t pid = fork();
    if (pid < 0) { perror("fork"); return 1; }

    if (pid > 0) {
        close(fd[0]);
        sort(a, n);

        dprintf(fd[1], "%d %d ", n, target);
        for (int i = 0; i < n; i++)
            dprintf(fd[1], "%d ", a[i]);

        close(fd[1]);
        wait(NULL);
    } else {
        close(fd[1]);

        char buffer[4096];
        ssize_t bytes = read(fd[0], buffer, sizeof(buffer) - 1);
        if (bytes <= 0) { perror("read"); exit(1); }
        buffer[bytes] = '\0';
        close(fd[0]);

        char *argv_exec[128];
        int argc = 0;
        char *tok = strtok(buffer, " \n");
        while (tok && argc < 127) {
            argv_exec[argc++] = tok;
            tok = strtok(NULL, " \n");
        }
        argv_exec[argc] = NULL;

        execve("./binary_search", argv_exec, environ);
        perror("execve");
        exit(1);
    }

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

This implementation uses two source files: `b2_parent.c` and `binary_search.c`. The parent sorts the array and sends the sorted data through a pipe; the child converts the received data into the argument list used by `execve()`, which loads the separate binary-search program.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 16.
