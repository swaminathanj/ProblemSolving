# Problem 4: Ehab and Another Construction Problem

## Problem 1088A-1

Given two numbers a and b, determine if a is divisible by b.

```
Input
Two integers a and b such that 1 ≤ a, b ≤ 100.

Output
Print "YES" if a is divisible by b. "NO" otherwise.

Example

Input
6 3

Output
YES

Input
6 4

Output
NO
```

### Solution Approach

It is trivial. When a divided by b does not leave a reminder, it is divisible. Otherwise it is not divisible.

### Implementation considerations
None

### Implementation
Define a function isdivisible that takes a and b as parameters and computes a%b. Return 1 or 0 based on the result. The main function reads a and b, calls isdivisible and based on the result, prints YES or NO.

``` c
// divisibility.c

#include <stdio.h>

int isdivisible(int a, int b) {
    if (a % b  == 0)
        return 1;
    else
        return 0;
}

int main() {
    int a, b;

    scanf("%d", &a);
    scanf("%d", &b);

    if ( isdivisible(a,b) )
        printf("YES\n");
    else
        printf("NO\n");

    return 0;
}
```

### Problem 1088A-2

Given three numbers a, b and x, determine if a is divisible by b and the product of a and b is greater than x.

```
Input
Three integers a, b and x such that 1 ≤ a, b, x ≤ 100.

Output
Print "YES" if a divides b and a * b > x. "NO" otherwise.

Example

Input
6 3 10

Output
YES

Input
6 4 10

Output
NO

Input
8 4 35

Output
NO
```

Note: 
 - In the first example, 6 is divisible by 3 and 6*3 = 18 > 10.
 - In the second example, 6 is not divisible by 4 although 6*4 = 24 > 10.
 - In the third example, 8 is divisible by 4 but 8*4 = 32 <35.
 
### Solution Approach

Trivial again. In addition to performing divisibility check, perform the multiplication and check if product is bigger.

### Implementation considerations
None

### Implementation
Define a function isproductbigger that takes a, b and x as parameters and checks if a*b > x. Return 1 or 0 based on the result. The main function reads a, b and x, calls isproductbigger and based on the result, prints YES or NO. The main calls both isdivisible and isproductbigger and prints "YES" only if both conditions are satisfied. Otherwise "NO".

``` c
// biggerproduct.c

#include <stdio.h>

int isdivisible(int a, int b) {
    if (a%b  == 0)
        return 1;
    else
        return 0;
}

int isproductbigger(int a, int b, int x) {
    if (a*b > x)
        return 1;
    else
        return 0;
}

int main() {
    int a, b, x;

    scanf("%d", &a);
    scanf("%d", &b);
    scanf("%d", &x);
 
    if ( isdivisible(a, b) && isproductbigger(a, b, x) )
        printf("YES\n");
    else
        printf("NO\n");    

    return 0;
}
```

## Problem 1088A-3

Given three numbers a, b and x, determine if a is divisible by b, the product of a and b is greater than x and the quotient of a / b is smaller than x.

```
Input
Three integers a, b and x such that 1 ≤ a, b, x ≤ 100.

Output
Print "YES" if a divides b, a * b > x and a / b < x. "NO" otherwise.

Example

Input
6 3 10

Output
YES

Input
6 3 1

Output
NO
```

### Solution Approach

Trivial again. In addition to performing divisibility and product checks, check if quotient is smaller.

### Implementation considerations
None

### Implementation
Define a function isquotientsmaller that takes a, b and x as parameters and checks if a/b < x. Return 1 or 0 based on the result. The main function reads a, b and x, calls isdivisible, isproductbigger and isquotientsmaller and based on the result, prints YES or NO.

``` c
// smallerquotient.c

#include <stdio.h>

int isdivisible(int a, int b) {
    if (a%b  == 0)
        return 1;
    else
        return 0;
}

int isproductbigger(int a, int b, int x) {
    if (a*b > x)
        return 1;
    else
        return 0;
}

int isquotientsmaller(int a, int b, int x) {
    if (a/b < x)
        return 1;
    else
        return 0;
}

int main() {
    int a, b, x;

    scanf("%d", &a);
    scanf("%d", &b);
    scanf("%d", &x);
 
    if ( isdivisible(a, b) && isproductbigger(a, b, x) && isquotientsmaller(a, b, x) )
        printf("YES\n");
    else
        printf("NO\n");    

    return 0;
}
```

## Problem 1088A-4

Given a number x, compute all permutations of (a, b) pairs such that 1 ≤ a, b ≤ x.

```
Input
An integer x such that 1 ≤ x ≤ 100.

Output
Print all permuations of numbers a and b that satisify the criteria 1 ≤ a, b ≤ x.

Example

Input
3

Output
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

### Solution Approach

Implement nested loop. In the outer loop a ranges from 1 to x and in the inner loop b ranges from 1 to x.

### Implementation considerations
None

### Implementation
Define a function generatepairs that takes x as a parameter, generates and prints all the pairs.

``` c
// generatepairs.c

#include <stdio.h>

void generatepairs(int x) {
    int a = 1;
    while (a <= x) {
        int b = 1;
        while (b <= x) {
            printf("%d %d\n", a, b);
            b++;
        }
        a++;
    }
}

int main() {
    int x;
    scanf("%d", &x);
    generatepairs(x);

    return 0;
}
```

## Problem 1088A-5

Given a number x, determine a pair (a, b) where 1 ≤ a, b ≤ x such that a is divisible by b, product of a and b is greater than x and quotient of a/b is less than x.

```
Input
An integer x such that 1 ≤ x ≤ 100.

Output
Print a pair a and b that satisify the above criteria. If no such pair exists, print -1. 
Note that there can be multiple pairs satisfying the criteria. You can print any valid pair.

Example

Input
3

Output
2 2

Input
10

Output
6 7
```

### Solution Approach

Implement nested loop. In the outer loop a ranges from 1 to x and in the inner loop b ranges from 1 to x. For each a, b pair check if b divides a, a * b > x and a/b < x.

### Implementation considerations
None

### Implementation
Define a function findpair that takes x as a parameter, generates and calls isdivisible, isproductbigger and isquotientsmaller on each pair. If all of them return positive, print that a and b and return. At the end of the loop print -1 (since we did not find any pair). The difference between findpair and generatepairs is that, findpair makes the additional check and prints only the pair that satisfy the criteria.

``` c
// findpair.c

#include <stdio.h>

int isdivisible(int a, int b) {
    if (a%b  == 0)
        return 1;
    else
        return 0;
}

int isproductbigger(int a, int b, int x) {
    if (a*b > x)
        return 1;
    else
        return 0;
}

int isquotientsmaller(int a, int b, int x) {
    if (a/b < x)
        return 1;
    else
        return 0;
}

void findpair(int x) {
    int a = 1;
    while (a <= x) {
        int b = 1;
        while (b <= x) {
            if ( isdivisible(a,b) && isproductbigger(a,b,x) && isquotientsmaller(a,b,x) ) {
                printf("%d %d\n", a, b);
                return;
            }
            b++;
        }
        a++;
    }
    printf("-1\n");
}

int main() {
    int x;
    scanf("%d", &x);
    findpair(x);

    return 0;
}
```

## Submission
 - Check out the problem 1088A Ehab and Another Construction Problem in [https://codeforces.com/problemset/problem/1088/A](https://codeforces.com/problemset/problem/1088/A)
 - After checking your program thoroughly, submit your solution and get an Accepted message.
