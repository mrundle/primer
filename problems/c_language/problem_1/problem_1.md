Write a C program that reads data from a file and then runs an interactive session (via stdin/stdout) allowing user queries. The program will take a filename as the first positional argument, and this input file will contain pairs of values, one pair per line. Each line will consist of a single “category” character A-Z, and a positive-integer “value” ranging from 0 to 2^64-1. The file can have an arbitrary number of total lines.  
```
A        1  
A        32  
B        9  
A        93  
C        1  
A        32  
C        1
```
Logically, the program should be storing these values in arrays, using one array per category. When reading this file into memory, the program will construct one array per category, and append each line’s value to that category’s array.  

```
/*  
 * textual representation of internal program state after reading the above file  
 *  
 * note: no need to use a hash table for this program, a linear search over  
 *       categories combined with direct indexing into the array will be fine  
 */  
[  
    ('A', [ 1, 32, 93, 32 ]),  
    ('B', [ 9 ]),  
    ('C', [ 1, 1 ]),  
]
```
After reading the input, the program will prompt the user for a category and an index. After receiving a category, the program will look up that category’s array, else indicate an error and restart the query loop. Upon successful array lookup, the program will prompt for an index, and then will print the value if that index in the array (else indicate an error).   
```
$ ./program numbers.txt  
Loaded numbers from numbers.txt.  
Category: Z                          # "Z" is user input
Invalid category  
Category: A                          # "A" is user input
Index: 999                           # "999" is user input
Invalid index for category A (need 0-3)  
Category: A                          # "A" is user input
Index: 0                             # "0" is user input
1  
Category: B                          # "B" is user input
Index: 0                             # "0" is user input
9  
...(and so on)...
```

A better example input file, with more lines, is here: [numbers.txt](https://pastebin.com/raw/sFfVCWTS). The program should be able to handle errors (invalid numbers, invalid arguments, memory faults), and should be able to run cleanly under valgrind (i.e. no memory leaks at program exit).  
  
Things that this example program will help practice:  

1.  Writing and compiling a C program with GCC
2.  Using command-line arguments
3.  Opening and reading from a file
4.  Reading and writing from the standard input
5.  Using different data types (`char`,  `uint64_t`)
6.  Allocating, re-allocating, and freeing heap memory
7.  Using pointers
8.  Running valgrind
9.  Core dumps and GDB (if any segfaults are encountered along the way)
