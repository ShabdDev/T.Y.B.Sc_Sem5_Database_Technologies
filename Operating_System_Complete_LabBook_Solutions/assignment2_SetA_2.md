# Assignment 2 — SetA — CPU Scheduling

## Question (as given in the lab book)

(ii) Write the program to simulate Non-preemptive Shortest Job First (SJF) -scheduling. The arrival time and first CPU-burst for different n number of processes should be input to the algorithm. Assume the fixed IO waiting time (2 units). The next CPU-burst should be generated randomly. The output should give Gantt chart, turnaround time and waiting time for each process. Also find the average waiting time and turnaround time.

## Solution

This solution is written in **C for Linux**, using standard POSIX/Linux system calls and libraries required by the practical.



### Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <time.h>

#define MAXP 20
#define IO_TIME 2

/*
 Algorithms:
 1 FCFS
 2 Non-preemptive SJF
 3 Preemptive SJF
 4 Non-preemptive Priority
 5 Preemptive Priority
 6 Round Robin
 The workbook says the next CPU burst is random but does not specify how
 many CPU bursts a process has. This implementation uses exactly two CPU
 bursts per process: the entered first burst and one randomly generated
 second burst, separated by 2 units of I/O.
*/

typedef struct {
    int id, arrival, priority;
    int burst[2], current_burst, rem;
    int state;       /* 0=not arrived, 1=ready, 2=I/O, 3=done, 4=running */
    int ready_since, io_until, completion, waiting;
    long ready_order;
} Process;

int better(Process *p, int a, int b, int alg) {
    if (b == -1) return 1;

    if (alg == 1 || alg == 6) {
        if (p[a].ready_order != p[b].ready_order)
            return p[a].ready_order < p[b].ready_order;
        return p[a].id < p[b].id;
    }
    if (alg == 2 || alg == 3) {
        if (p[a].rem != p[b].rem) return p[a].rem < p[b].rem;
        return p[a].id < p[b].id;
    }
    if (alg == 4 || alg == 5) {
        if (p[a].priority != p[b].priority)
            return p[a].priority < p[b].priority; /* 1 = highest */
        return p[a].id < p[b].id;
    }
    return 0;
}

int choose_ready(Process p[], int n, int alg) {
    int best = -1;
    for (int i = 0; i < n; i++)
        if (p[i].state == 1 && better(p, i, best, alg))
            best = i;
    return best;
}

int choose_preemptive(Process p[], int n, int current, int alg) {
    int best = current;
    if (best == -1) best = choose_ready(p, n, alg);

    for (int i = 0; i < n; i++) {
        if (p[i].state == 1 && better(p, i, best, alg))
            best = i;
    }
    return best;
}

void print_gantt(int gp[], int gs[], int ge[], int gc) {
    printf("\nGantt Chart:\n");
    if (gc == 0) { printf("(no CPU execution)\n"); return; }

    for (int i = 0; i < gc; i++)
        printf("| P%d (%d-%d) ", gp[i] + 1, gs[i], ge[i]);
    printf("|\n");
}

int main(void) {
    int n, alg, quantum = 0;
    Process p[MAXP];

    printf("Choose algorithm:\n");
    printf("1. FCFS\n2. Non-preemptive SJF\n3. Preemptive SJF\n");
    printf("4. Non-preemptive Priority\n5. Preemptive Priority\n6. Round Robin\n");
    printf("Enter choice: ");
    scanf("%d", &alg);

    printf("Enter number of processes: ");
    scanf("%d", &n);

    if (n <= 0 || n > MAXP) {
        printf("Invalid number of processes.\n");
        return 1;
    }

    if (alg == 6) {
        printf("Enter time quantum: ");
        scanf("%d", &quantum);
        if (quantum <= 0) return 1;
    }

    srand(42); /* fixed seed makes the random second burst reproducible */

    for (int i = 0; i < n; i++) {
        p[i].id = i;
        printf("\nP%d arrival time and first CPU burst: ", i + 1);
        scanf("%d%d", &p[i].arrival, &p[i].burst[0]);

        if (alg == 4 || alg == 5) {
            printf("P%d priority (1 = highest): ", i + 1);
            scanf("%d", &p[i].priority);
        } else {
            p[i].priority = 0;
        }

        p[i].burst[1] = 1 + rand() % 9;
        p[i].current_burst = 0;
        p[i].rem = p[i].burst[0];
        p[i].state = 0;
        p[i].ready_since = p[i].arrival;
        p[i].ready_order = 0;
        p[i].io_until = 0;
        p[i].completion = -1;
        p[i].waiting = 0;
    }

    printf("\nGenerated second CPU bursts (after %d units I/O):\n", IO_TIME);
    for (int i = 0; i < n; i++)
        printf("P%d: first=%d, second=%d\n",
               i + 1, p[i].burst[0], p[i].burst[1]);

    int done = 0, t = 0, current = -1, slice = 0;
    long ready_counter = 0;
    int gp[10000], gs[10000], ge[10000], gc = 0;

    while (done < n && t < 10000) {
        /* Arrivals */
        for (int i = 0; i < n; i++) {
            if (p[i].state == 0 && p[i].arrival <= t) {
                p[i].state = 1;
                p[i].ready_since = p[i].arrival;
                p[i].ready_order = ready_counter++;
            }
            if (p[i].state == 2 && p[i].io_until <= t) {
                p[i].state = 1;
                p[i].ready_since = t;
                p[i].ready_order = ready_counter++;
            }
        }

        /* Select / preempt */
        if (current == -1) {
            current = choose_ready(p, n, alg);
            if (current != -1) {
                p[current].state = 4;
                slice = 0;
            }
        } else if (alg == 3 || alg == 5) {
            int best = choose_preemptive(p, n, current, alg);
            if (best != current) {
                p[current].state = 1;
                p[current].ready_since = t;
                p[current].ready_order = ready_counter++;
                current = best;
                p[current].state = 4;
                slice = 0;
            }
        }

        if (current == -1) {
            t++;
            continue;
        }

        /* Every ready process waits for this one time unit. */
        for (int i = 0; i < n; i++)
            if (p[i].state == 1) p[i].waiting++;

        /* Add/extend Gantt segment. */
        if (gc == 0 || gp[gc - 1] != current || ge[gc - 1] != t) {
            gp[gc] = current;
            gs[gc] = t;
            ge[gc] = t + 1;
            gc++;
        } else {
            ge[gc - 1] = t + 1;
        }

        p[current].rem--;
        slice++;
        t++;

        if (p[current].rem == 0) {
            if (p[current].current_burst == 0) {
                p[current].current_burst = 1;
                p[current].rem = p[current].burst[1];
                p[current].state = 2;
                p[current].io_until = t + IO_TIME;
                current = -1;
            } else {
                p[current].state = 3;
                p[current].completion = t;
                done++;
                current = -1;
            }
        } else if (alg == 6 && slice == quantum) {
            p[current].state = 1;
            p[current].ready_since = t;
            p[current].ready_order = ready_counter++;
            current = -1;
        }
    }

    print_gantt(gp, gs, ge, gc);

    double avg_wt = 0, avg_tat = 0;
    printf("\nPID\tArrival\tBurst1\tBurst2\tCompletion\tWaiting\tTurnaround\n");
    for (int i = 0; i < n; i++) {
        int tat = p[i].completion - p[i].arrival;
        avg_wt += p[i].waiting;
        avg_tat += tat;
        printf("P%d\t%d\t%d\t%d\t%d\t\t%d\t%d\n",
               i + 1, p[i].arrival, p[i].burst[0], p[i].burst[1],
               p[i].completion, p[i].waiting, tat);
    }

    printf("\nAverage waiting time = %.2f\n", avg_wt / n);
    printf("Average turnaround time = %.2f\n", avg_tat / n);
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

When the program starts, select option **2** for this question.

The workbook does not specify how many CPU bursts each process should have. To make the simulation executable without inventing an input field, this implementation uses **two CPU bursts per process**: the entered first CPU burst and one randomly generated second CPU burst, separated by the specified 2-unit I/O wait. The random generator uses a fixed seed (`42`) so the generated second bursts are reproducible during lab verification.

For this file, select the algorithm corresponding to the question:
- Set A, Q1 → option `1`
- Set A, Q2 → option `2`
- Set B, Q1 → option `3`
- Set B, Q2 → option `4`
- Set C, Q1 → option `5`
- Set C, Q2 → option `6`

## Important points

- The question is reproduced above before the solution.
- The program is designed for a Linux environment, as specified by the workbook.
- Use `Ctrl+C` only when you intentionally need to stop a long-running process.
- For algorithms, enter the input requested by the program and verify the displayed intermediate/result values.

**Lab-book source:** CS-305-MJ-P Operating Systems Workbook, page 23.
