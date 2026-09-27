# Assignment 1 — Set B — Question 1: Orphan Process

## Question (as given in the lab book)

(1) Write a C program to illustrate the concept of orphan process. Parent process creates a child and terminates before child has finished its task. So child process becomes orphan process. (Use fork(), sleep(), getpid(), getppid()).

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <stdlib.h>

int main(void) {
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        return 1;
    }

    if (pid > 0) {
        printf("Parent: PID = %d, child PID = %d\n", getpid(), pid);
        printf("Parent terminates before child finishes.\n");
        return 0;
    }

    printf("Child: PID = %d, Parent PID = %d\n", getpid(), getppid());
    sleep(5);
    printf("Child after sleep: PID = %d, new Parent PID = %d\n",
           getpid(), getppid());
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

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 16.
