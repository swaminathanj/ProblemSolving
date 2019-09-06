# Problem 1017A

## Problem 1017A-1

A student by name Thomas Smith took 4 exams English, German, Maths and History. His father John Smith wants to compute the total marks obtained by Thomas. Please help John find the total.

```
Input
Four space-separated integers with values between the range 0 and 100 -- the marks obtained in each subject.

Output
Total marks obtained by Thomas.

Example

Input
100 98 99 100

Output
397
```

Note: The solution is trivial and therefore not described. Implement the program and check with different test cases.

## Problem 1017A-2

A small rephrase of the problem is that Thomas took k exams instead of fixed 4. His father John Smith wants to compute the total marks obtained by Thomas. Please help John find the total.

```
Input
The first line gives the value of k
The second line contains k space-separated integers with values between the range 0 and 100 -- the marks obtained in each subject.

Output
Total marks obtained by Thomas.

Example

Input
4
100 98 99 100

Output
397
```

### Solution Approach

Use a variable to accumulate the marks as you read them from keyboard in a loop.

### Implementation considerations
None

### Implementation
We will implement a function findsum that defines an accumulator variable sum initially set to 0. As the marks are read they are added to sum. The main will read k and call findsum. In order for findsum to know how many marks to read, main will pass k as a parameter to findsum.

An accumulator variable + a loop is a common way of computing a result in a progressive fashion. After first i iterations, the variable will hold the sum of first i numbers.

``` c
// findsum.c

#include <stdio.h>

int findsum(int count) {
    int sum = 0; // initialized to 0
    int temp; // a temporary variable to hold the marks just read

    int i = 0;
    while (i < count) {
       scanf("%d", &temp); 
       sum = sum + temp;  // add temp to existing sum
       i++;
    }
    return sum;
}

int main() {
    int k, sum;
    scanf("%d", &k);

    sum = findsum(k);

    printf("%d\n", sum);

    return 0;
}
```

### Remarks

What does: sum = sum + temp; mean? In math, we never to such a thing. It seems like cyclic-dependency and outright absurd. In computer science it is not so. When you compile the program, this statement will break down into multiple machine language statements.

```
load sum R1     // Load the value of sum (the one in rhs) to register R1 in the CPU
load temp R2    // Load the value of temp to register R2 in the CPU
iadd R1 R2       // Integer addition of contents in R1 and R2. The result will be in R1. The CPU is wired that way.
store R1 sum    // Copy the value of register R1 of CPU to location/address of sum (the one in lhs)
```

As you see, a variable on the rhs refers to its value while the variable on the rhs refers to its address. On the rhs, we are interested in the value of sum so as to do our computation whereas on the lhs, we are interested in its address to store the result of our computation.

### Testing

Try with different values for k and different set of marks for k subjects.

## Problem 1017A-3

Given total marks of n students John wants to find who got the highest. In other words who got the first rank.

```
Input
The first line gives the number of students n where 1 <= n <= 100.
The n lines that follow contain the total marks obtained by the n students. The total marks does not exceed 1000.

Output
The student with the highest total (denoted by the index).

Example

Input
6
434
410
396
448
455
423

Output
5
```

Note: The fifth one with total marks as 455 is the highest

### Solution Approach

Initially assume the first one is the highest and set topper to 1. Loop through from 2 to n and whenever any mark is greater than the (current) highest, reassign highest and topper.

### Implementation considerations
None

### Implementation
We will implement a function findtopper which will read the marks and reset highest and topper as necessary.

``` c
// findtopper.c

#include <stdio.h>

int findtopper(int num) {
    int mark;
    scanf("%d", &mark); // Read mark of first student

    int topper = 1;
    int highest = mark;

    int i = 2; // loop from the second one
    while (i <= num) {
        scanf("%d", &mark);
        if (mark > highest) {
            highest = mark; // highest marks and
            topper = i;     // topper reassigned
        }
        i++;
    }
    return topper;
}

int main() {
    int n;
    scanf("%d", &n);

    int topper = findtopper(n);

    printf("%d\n", topper);
    return 0;
}
```

## Problem 1017A-4

Given individual marks of 4 subjects for n students John wants to find who got the highest. In other words who got the first rank.

```
Input
The first line gives the number of students n where 1 <= n <= 100.
The n lines that follow contain 4 integers denoting the marks obtained by each student. The total marks does not exceed 1000.

Output
The student with the highest total (denoted by the index).

Example

Input
6
90 80 95 75
60 90 70 100
80 65 90 75
100 80 78 90
85 100 85 95
70 93 90 80

Output
5
```

Note: The fifth one with total marks as 365 is the higher than all other marks.

### Solution Approach

We have the function findtopper that computes the topper given total marks of n students. We have one more function findsum that computes the total marks given individual marks. findtopper has to be modified to use findsum to compute the total marks.

### Implementation considerations
None

### Implementation
We will modify the function findtopper (call it computetopper) which will use findsum to compute the total and reset highest and topper as necessary.

```
// computetopper.c

#include <stdio.h>

int findsum(int count) {
    int sum = 0; // accumulator variable
    int temp; // a temporary variable to hold the marks just read

    int i = 0;
    while (i < count) {
       scanf("%d", &temp); 
       sum = sum + temp;  // add temp to existing sum
       i++;
    }
    return sum;
}

int computetopper(int num) {
    int mark;
    //scanf("%d", &mark); // Read mark of first student
    mark = findsum(4);  // Compute sum of first student marks

    int topper = 1;
    int highest = mark;

    int i = 2; // loop from the second one
    while (i <= num) {
        //scanf("%d", &mark); // Read mark of i-th student
        mark = findsum(4); // Compute sum of i-th student marks
        if (mark > highest) {
            highest = mark; // highest marks and
            topper = i;     // topper reassigned
        }
        i++;
    }
    return topper;
}

int main() {
    int n;
    scanf("%d", &n);

    int topper = computetopper(n);

    printf("%d\n", topper);
    return 0;
}
```

### Remarks
 - The only difference between findsum and computesum is line numbers 18 and 26 are replaced by 19 and 27. i.e. instead of reading the total sum through scanf, they compute the sum through findsum.
Since the problem is about marks of 4 subjects, the parameter passed to findsum is 4.

## Problem 1017A-5

Given individual marks of 4 subjects for n students, John wants to find the rank of Thomas. The marks of Thomas is listed first followed by the marks of other students.

```
Input
The first line contains an integer n 1 <= n <= 100 -- that denotes the number of students where.
The n lines that follow contain 4 integers denoting the marks obtained by each student. The first line being the marks of Thomas. The total marks does not exceed 1000.

Output
The rank of Thomas.

Example

Input
6
90 80 95 75
60 90 70 100
80 65 90 75
100 80 78 90
85 100 85 95
70 93 90 80

Output
3
```

Note: The total marks adds up to 340, 320, 310, 348, 365 and 333 for n students respectively. Thomas has scored the third highest and hence his rank is 3.

### Solution Approach

We have a function findsum that computes the total marks given individual marks. We can use it once to find the total marks obtained by Thomas. We set the rank of Thomas to 1. We then iterate through and compute the total marks of rest of the students and whenever the total marks of a student exceeds that of Thomas, we increase his rank by 1.

### Implementation considerations
None

Implementation
We will implement the function findrank which will  use findsum to compute the total and reset Thomas' rank as necessary. The implementation of findrank is pretty similar to computetotal except that, in findrank the total marks of other students is compared with Thomas' total marks instead of comparing against the current highest.

The code is not given. Try to do it yourself.

## Submission
 - Check out the problem 1017A The Rank in [https://codeforces.com/problemset/problem/1017/A](https://codeforces.com/problemset/problem/1017/A)
 - After checking your program thoroughly, submit your solution and get an Accepted message.
