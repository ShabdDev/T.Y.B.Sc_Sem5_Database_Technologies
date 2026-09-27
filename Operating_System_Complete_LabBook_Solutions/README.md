# CS-305-MJ-P Operating Systems — Complete Lab Book Solutions

This folder contains the complete C/Linux solutions for **all six assignments** in the uploaded SPPU T.Y.B.Sc. Computer Science Operating Systems practical workbook.

## Lab-book structure

The workbook divides the practical syllabus into six assignments:

1. Operations on Processes
2. CPU Scheduling
3. Memory Management Methods
4. Banker's Algorithm
5. File Allocation Methods
6. Disk Scheduling Algorithms

Each assignment is divided into Sets A, B and C. Set A is mandatory in the workbook, while Sets B and C provide additional variations/deeper practice.

## Files

### Assignment 1 — Operations on Processes
- `assignment1_SetA_1.md` — nice() system call
- `assignment1_SetA_2.md` — fork(), bubble sort, insertion sort and wait()
- `assignment1_SetB_1.md` — orphan process
- `assignment1_SetB_2.md` — execve() and binary search
- `assignment1_SetC_1.md` — shell with count command
- `assignment1_SetC_2.md` — shell with search command

### Assignment 2 — CPU Scheduling
- `assignment2_SetA_1.md` — FCFS
- `assignment2_SetA_2.md` — Non-preemptive SJF
- `assignment2_SetB_1.md` — Preemptive SJF
- `assignment2_SetB_2.md` — Non-preemptive Priority
- `assignment2_SetC_1.md` — Preemptive Priority
- `assignment2_SetC_2.md` — Round Robin

### Assignment 3 — Memory Management
- `assignment3_SetA_1.md` — FIFO + LRU
- `assignment3_SetB_1.md` — MFU + Optimal
- `assignment3_SetC_1.md` — FIFO + LRU + MFU + Optimal comparison

### Assignment 4 — Banker's Algorithm
- `assignment4_SetA_1.md` — Need matrix
- `assignment4_SetB_1.md` — Safety algorithm
- `assignment4_SetC_1.md` — Resource-request algorithm

### Assignment 5 — File Allocation
- `assignment5_SetA_1.md` — Contiguous allocation
- `assignment5_SetB_1.md` — Linked allocation
- `assignment5_SetC_1.md` — Indexed allocation

### Assignment 6 — Disk Scheduling
- `assignment6_SetA_1.md` — FCFS
- `assignment6_SetA_2.md` — SSTF
- `assignment6_SetB_1.md` — SCAN
- `assignment6_SetB_2.md` — LOOK
- `assignment6_SetC_1.md` — Comparative FCFS/SSTF/SCAN/LOOK

## Software requirements

The workbook specifies:
- Linux operating system
- Any Linux-based editor such as `vi` or `gedit`
- `cc` or `gcc` compiler

Recommended compilation command used in these solutions:

```bash
gcc -std=c11 -Wall -Wextra program.c -o program
```

## Important implementation note — Assignment 2

The workbook says that the next CPU burst should be generated randomly and that I/O waiting time is fixed at 2 units, but it does not specify how many CPU bursts each process should execute.

To make the simulation concrete and reproducible, the supplied solution uses:
- first CPU burst = user input
- one randomly generated second CPU burst
- I/O waiting time = 2 units
- fixed random seed = 42

The Assignment 2 program is a single scheduler implementation with an algorithm-selection menu. Each markdown file tells you which option to select for that particular lab-book question.

## Important implementation note — File Allocation

The workbook's bit-vector example treats `1` as a free block and `0` as an allocated block. The solutions follow that convention.

## Important implementation note — Banker's Algorithm

- Set A computes and displays `Need = Max - Allocation`.
- Set B additionally accepts `Available` and executes the Safety Algorithm.
- Set C derives `Available` from total instances and current allocation, checks a resource request against `Need` and `Available`, tentatively allocates it, and then performs a safety check.

## Important implementation note — Disk Scheduling

For SCAN and LOOK, the programs ask for direction:
- `0` = left
- `1` = right

SCAN travels to the physical disk end before reversing.
LOOK reverses at the last pending request in the current direction.

