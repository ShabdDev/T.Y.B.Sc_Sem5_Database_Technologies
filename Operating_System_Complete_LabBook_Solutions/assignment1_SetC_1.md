# Assignment 1 — Set C — Question 1: Shell with count Command

## Question (as given in the lab book)

(1) Write a C program that behaves like a shell which displays the command prompt as $ or #. It accepts the command, tokenize the command line and execute it by creating the child process. Also implement the additional command ‘count’ as

$ count c filename: It will display the number of characters in given file.

$ count w filename : It will display the number of words in given file.

$ count l filename : It will display the number of lines in given file.

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

void count_file(char mode, const char *filename) {
    FILE *fp = fopen(filename, "r");
    if (!fp) { perror(filename); return; }

    long chars = 0, words = 0, lines = 0;
    int c, in_word = 0;

    while ((c = fgetc(fp)) != EOF) {
        chars++;
        if (c == '\n') lines++;
        if (c == ' ' || c == '\t' || c == '\n' || c == '\r' || c == '\f' || c == '\v')
            in_word = 0;
        else if (!in_word) {
            in_word = 1;
            words++;
        }
    }
    fclose(fp);

    if (mode == 'c') printf("Characters: %ld\n", chars);
    else if (mode == 'w') printf("Words: %ld\n", words);
    else if (mode == 'l') printf("Lines: %ld\n", lines);
    else printf("Invalid count option.\n");
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
    char line[MAXLINE];
    char *args[MAXARGS];

    while (1) {
        printf("$ ");
        fflush(stdout);

        if (!fgets(line, sizeof(line), stdin)) break;
        int argc = tokenize(line, args);
        if (argc == 0) continue;
        if (strcmp(args[0], "q") == 0) break;

        if (strcmp(args[0], "count") == 0) {
            if (argc != 3) {
                printf("Usage: count c|w|l filename\n");
                continue;
            }
            count_file(args[1][0], args[2]);
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
count c sample.txt
count w sample.txt
count l sample.txt
ls
pwd
q
```

The shell uses `fork()` and `execvp()` for normal commands and handles `count` internally.

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 16.
