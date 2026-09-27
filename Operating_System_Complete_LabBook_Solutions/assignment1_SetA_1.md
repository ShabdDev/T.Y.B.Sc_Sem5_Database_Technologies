# Assignment 1 — Set A — Question 1: nice() System Call

## Question (as given in the lab book)

(1) Write a program that demonstrates the use of nice() system call. After a child process is started using fork(), assign higher priority to the child using nice() system call.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <sys/resource.h>
#include <errno.h>
#include <string.h>

int main(void) {
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        return 1;
    }

    if (pid == 0) {
        int old_nice = getpriority(PRIO_PROCESS, 0);
        printf("Child PID = %d\n", getpid());
        printf("Child nice value before change = %d\n", old_nice);

        /* -5 requests a higher CPU priority. A normal user may need sudo. */
        errno = 0;
        if (setpriority(PRIO_PROCESS, 0, -5) == -1) {
            perror("setpriority(-5)");
            printf("Run the program with appropriate privileges if your system denies a negative nice value.\n");
        }

        printf("Child nice value after change = %d\n",
               getpriority(PRIO_PROCESS, 0));
        return 0;
    }

    wait(NULL);
    printf("Parent PID = %d: child has completed.\n", getpid());
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

**Note:** On Linux, decreasing the nice value (for example from 0 to -5) increases CPU priority and normally requires suitable privileges. If `setpriority()` reports `Permission denied`, run the executable with `sudo` in a lab environment where that is permitted.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 15.
