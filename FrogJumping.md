# Frog Jumping (1077A)

## Problem 1077A-1

A frog is currently at point 0 on the x-axis. It jumps a units to the right. Your task is to calculate the position of the frog after k jumps.

```
Input
Two integers a, k such that 1 ≤  a, k  ≤  10^9, the jump length and the number of jumps.

Output
The current position of the frog.

Example

Input
5 3

Output
15
```

Note: The frog reaches 15 (0 --> 5 --> 10 --> 15) in 3 jumps.

### Solution Approach

It is easy to infer that the solution is k times a (or product of a and k).

### Implementation considerations
The problem states that the values of a and k range from 0 to 10^9. This is important to determine which data type to use for a and k. Let's say we chose to use unsigned int for both a and k. Is it big enough to accommodate them?

Let's do a quick and dirty calculation.

 - 2^10/1024 is approximately equal to 10^3/1000. So 10^9 would be about 2^30. The largest value stored by an unsigned int is given by UINT_MAX, which is 2^32 - 1. Hence, unsigned int seems a good data type for a and k.
 - But wait!! If both a and k happen to be 10^9, the product would be 10^18. Can unsigned int hold the result? If it can't we will end up computing an incorrect product due to overflow.
 - 10^18 would be about 2^60. An unsigned int cannot never accommodate such a huge number. We need to use long or unsigned long.
Since a and k are both positive, the product would be positive too. Hence, we will go for unsigned long. 
Implementation
We will implement a function rjump for computing the current position, given jump length (right) and number of jumps (jumps). The main will read a and k, make a function call to rjump and print the returned result (current).

``` c
// rjump.c

#include <stdio.h>

unsigned long rjump(unsigned long right, unsigned long jumps) {
    return right * jumps;
}

int main() {

    unsigned long a, k, current=0; // variable declaration

    scanf("%lu", &a);    // read a
    scanf("%lu", &k);    // read k

    current = rjump(a, k);    // function call to compute

    printf("%lu\n", current);    // print output
}
```

### Testing

You may want to run the program with different test cases to make sure your program works properly. Especially the corner cases.

#### Inputs
```
5 10
12345 67890
1000000000 5
5 1000000000
1000000000 1000000000
```

Note: It is enough to try inputs according to the given input specification. For example, since a, k are in the range 1 to 10^9, it is not necessary to try for 0 or negative values. One may possibly get inappropriate answers for such values. It is fine.

## Problem 1077A-2

A modified version of the problem is that the frog jumps to the left. Starting at point 0 on the x-axis, it jumps b units to the left. Your task is to calculate the position of the frog after k jumps.

```
Input 
Two integers b, k such that 1 ≤  b, k  ≤  10^9, the jump length and the number of jumps.

Output
The current position of the frog.

Example

Input
5 4

Output
-20
```

Note: The frog reaches -20 (0 --> -5 --> -10 --> -15 --> -20) in 4 jumps.

### Solution Approach

It is easy to infer that the solution is the negative of the product of b and k. So, it is easier to use the above implementation and make minor changes.

### Implementation considerations
Since b and k are in the range 0 to 109 and we are to compute the negative of their product, unsigned long is not appropriate. So we use long instead. The long covers the range of -263 to 263 - 1 which can accommodate the maximum value of -1018 (or -260). 

### Implementation
We will implement a function ljump for computing the current position, given jump length (left) and number of jumps (jumps). The main will read b and k, make a function call to ljump and print the returned result (current).

``` c
// ljump.c

#include <stdio.h>

long ljump(long left, long jumps) {
    return left * jumps * -1;
}

int main() {

    long b, k, current=0; // variable declaration

    scanf("%ld", &b);    // read b 
    scanf("%ld", &k);    // read k

    current = ljump(b, k);    // function call to compute

    printf("%ld\n", current);    // print output
}
```

### Testing

Again try the program with different test cases to make sure your program works properly. Especially the corner cases. Check if you get the output as expected.

### Problem 1077A-3

We twist the problem even further now. Starting at point 0 on the x-axis, it jumps a units to the right, then b units to the left, then right, then left and so on. Your task is to calculate the position of the frog after k jumps.

```
Input
Three integers a, b, k such that 1 ≤  a, b, k  ≤  109, the jump lengths in right and left directions and the number of jumps.

Output
The current position of the frog.

Example

Input
5 3 4

Output
4
```

Note: The frog reaches 4 (0 --> 5 --> 2 --> 7 --> 4) in 4 jumps.

### Solution Approach

This solution to the problem has 2 cases.

 1. If k is even, the frog jumps right half the number of times and jumps left the remaining half. So, sum up a*k/2 and b*k/2.
 2. If k is odd, the frog would take an extra jump to the right when compared to the left. So, sum up a*(k-1)/2, b*(k-1)/2 and a.

### Implementation considerations

If k is odd, k/2 would actually return (k-1)/2. For example, if k = 5, k/2 would be 2 since k is long. Try and check it out.
Note: Floating point computation will not automatically happen. Moreover, FP arithmetic is entirely different from integer arithmetic and can be done only on floating point numbers/variables.

### Implementation
The logic of rjump and ljump can be used by rljump to accomplish the task. We will implement a function rljump which will first check if k is odd or even and accordingly perform the required computation. The main will read a, b and k, make a function call to rljump and print the returned result (current).

``` c
// rljump.c

#include <stdio.h>

long rjump(long right, long jumps) {
    return right*jumps;
}

long ljump(long left, long jumps) {
    return -1*left*jumps;
}

long rljump(long right, long left, long jumps) {
    if (jumps%2 == 0) {     // jumps is even
        return rjump(right,jumps/2) + ljump(left,jumps/2);
    }
    else {    // jumps is odd
        return rjump(right,jumps/2) + ljump(left,jumps/2) + right;
    }
}

int main() {
    long a, b, k, current=0; // variable declaration

    scanf("%ld", &a);    // read a 
    scanf("%ld", &b);    // read b 
    scanf("%ld", &k);    // read k

    current = rljump(a, b, k);    // function call to compute

    printf("%ld\n", current);    // print output
}
```

### Testing

Try with different test cases.

## Problem 1077A-4

The previous program can compute the current position for only one test input. A sophisticated version of the above problem would be to compute the current position of the frog for multiple test inputs or queries. Suppose there are t queries, where a, b and k are different for each query, your task is to calculate the position of the frog after k jumps for all the t test cases.

```
Input
 - The first line of the input contains one integer t (1 ≤  t  ≤  1000) -- the number of test cases or queries
 - Each of the next t lines contain queries -- one query per line.
 - The query is described as three space-separated integers a, b, k such that 1 ≤  a, b, k  ≤  109, the jump lengths in right and left directions and the number of jumps.

Output
 - Print t integers. The i-th integer should be answer of i-th query. The current position of the frog.

Example

Input
6
5 3 4
100 1 4
1 10 5
1000000000 1 6
1 1 1000000000
1 1 999999999

Output
4
198
-17
2999999997
0
1
```

Note
- In the first query frog jumps 5 to the right, 2 to the left and 5 to the right so the answer is 5−2+5=8.
- In the second query frog jumps 100 to the right, 1 to the left, 100 to the right and 1 to the left so the answer is 100−1+100−1=198.
- In the third query the answer is 1−10+1−10+1=−17.
- In the fourth query the answer is 109−1+109−1+109−1=2999999997.
- In the fifth query all frog's jumps are neutralised by each other so the answer is 0.
- The sixth query is the same as the fifth but without the last jump so the answer is 1.

### Solution

Since we have the core solution implemented in the form of rljump, we just have to repeat it for all queries.

 - We first read the number of queries t using scanf().
 - Repeat the following for t times:
 - Read input a, b, k using scanf().
 - Compute the position by calling the function rljump().
 - Print the position using printf().

### Implementation considerations
t ranges from 1 to 1000 an integer type would be more than enough.

The implementation is given below.

``` c
// frogjump.c

#include <stdio.h>

long rjump(long right, long jumps) {
    return right*jumps;
}

long ljump(long left, long jumps) {
    return -1*left*jumps;
}

long rljump(long right, long left, long jumps) {
    if (jumps%2 == 0) {     // jumps is even
        return rjump(right,jumps/2) + ljump(left,jumps/2);
    }
    else {    // jumps is odd
        return rjump(right,jumps/2) + ljump(left,jumps/2) + right;
    }
}

int main() {
    int t, i=0;
    long a, b, k, current=0; // variable declaration

    scanf("%d", &t);

    while (i < t) {

        scanf("%ld", &a);    // read a 
        scanf("%ld", &b);    // read b 
        scanf("%ld", &k);    // read k

        current = rljump(a, b, k);    // function call to compute

        printf("%ld\n", current);    // print output
        i++;
    }
    return 0;
}
```
## Submission
 - Check out the problem 1077A Frog Jumping in https://codeforces.com/problemset/problem/1077/A
 - After checking your program thoroughly, submit your solution and get an Accepted message.

## A cautionary note

 - In older 32-bit machines, long is 32 bits only. In such a case, your submission may compute incorrect result in the test machine and solution may not be accepted. 
 - It is safer to use long long instead. (i.e. long long a, b, k, ...). The format specifier for reading/writing long long variable is "%lld" (el-el-d) on linux systems and "%I64d" (EYE-64-d) on Windows systems.
Perhaps the program that would eventually be accepted by code forces would be of the following form with above two changes implemented.

``` c
// frogjump_cf.c

#include <stdio.h>

long long rjump(long long right, long long jumps) {
    return right*jumps;
}

long long ljump(long long left, long long jumps) {
    return -1*left*jumps;
}

long long rljump(long long right, long long left, long long jumps) {
    if (jumps%2 == 0) {     // jumps is even
        return rjump(right,jumps/2) + ljump(left,jumps/2);
    }
    else {    // jumps is odd
        return rjump(right,jumps/2) + ljump(left,jumps/2) + right;
    }
}

int main() {
    int t, i=0;
    long long a, b, k, current=0; // variable declaration

    scanf("%d", &t);

    while (i < t) {

        scanf("%I64d", &a);    // read a 
        scanf("%I64d", &b);    // read b 
        scanf("%I64d", &k);    // read k

        current = rljump(a, b, k);    // function call to compute

        printf("%I64d\n", current);    // print output
        i++;
    }
    return 0;
}
```
