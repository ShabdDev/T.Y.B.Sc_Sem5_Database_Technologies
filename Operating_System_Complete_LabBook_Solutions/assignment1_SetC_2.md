# Assignment 1 — Set C — Question 2: Shell with search Command

## Question (as given in the lab book)

(2) Write a C program that behaves like a shell which displays the command prompt as $ or #. It accepts the command, tokenize the command line and execute it by creating the child process. Also implement the additional command ‘search’ as

$ search f filename pattern : It will search the first occurrence of pattern in the given file.

$ search a filename pattern: It will search all the occurrence of pattern in the given file.

$ search c filename pattern: It will count the number of occurrence of pattern in the given file.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

#define MAXLINE 1024
#define MAXARGS 64

void search_file(char mode, const char *filename, const char *pattern) {
    FILE *fp = fopen(filename, "r");
    if (!fp) { perror(filename); return; }

    char line[4096];
    long count = 0, line_no = 0;

    while (fgets(line, sizeof(line), fp)) {
        line_no++;
        char *p = line;
        int found_on_line = 0;

        while ((p = strstr(p, pattern)) != NULL) {
            count++;
            found_on_line = 1;
            if (mode == 'f') {
                printf("First occurrence at line %ld: %s", line_no, line);
                fclose(fp);
                return;
            }
            p += 1; /* allows overlapping matches */
        }

        if (mode == 'a' && found_on_line)
            printf("Line %ld: %s", line_no, line);
    }
    fclose(fp);

    if (mode == 'a') printf("Total occurrences: %ld\n", count);
    else if (mode == 'c') printf("Occurrences: %ld\n", count);
    else if (mode != 'f') printf("Invalid search option.\n");
    else printf("Pattern not found.\n");
}

int tokenize(char *line, char *args[]) {
    int n = 0;
    char *tok = strtok(line, " \t\n");
    while (tok && n < MAXARGS - 1) {
        args[n++] = tok;
        tok = strtok(NULL, " \t\n");
    }
    args[n] = NULL;
    return n;
}

int main(void) {
    char line[MAXLINE], *args[MAXARGS];

    while (1) {
        printf("$ ");
        fflush(stdout);

        if (!fgets(line, sizeof(line), stdin)) break;
        int argc = tokenize(line, args);
        if (argc == 0) continue;
        if (strcmp(args[0], "q") == 0) break;

        if (strcmp(args[0], "search") == 0) {
            if (argc != 4) {
                printf("Usage: search f|a|c filename pattern\n");
                continue;
            }
            search_file(args[1][0], args[2], args[3]);
            continue;
        }

        pid_t pid = fork();
        if (pid < 0) { perror("fork"); continue; }

        if (pid == 0) {
            execvp(args[0], args);
            perror("execvp");
            exit(1);
        }
        waitpid(pid, NULL, 0);
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

Try commands such as:

```text
search f sample.txt Linux
search a sample.txt Linux
search c sample.txt Linux
ls
q
```

The `search` command is implemented inside the shell; other commands are executed through a forked child and `execvp()`.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 16.
