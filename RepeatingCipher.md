# Problem 1095A: Repeating Cipher

## Problem 1095A-1

Consider a string of characters of length n. You have to print alternate characters.

```
Input
The first line contains n (1 ≤ n ≤ 55) -- the length of the string.
The second line contains the string of chars.

Output
Print alternate chars of the string.

Example

Input
10
abcdefghij

Output
acegi
```

### Solution Approach

Read a char, skip the next one. Repeat this till all the chars are read.

### Implementation considerations
None

### Implementation
Repeatedly read chars. If the position is odd, print it. 

``` c
// oddchars.c

#include <stdio.h>

int main() {
    int n;
    scanf("%d\n", &n); // \n is important as we are going to read char next
                       // Otherwise first char read will be '\n', not input

    char ch;
    int i = 1;
    while (i <= n) {
        scanf("%c", &ch);   // read a char
        if ( i%2 == 1)    // odd position
            printf("%c", ch);
        i++;
    }
    printf("\n"); // a newline
    
    return 0;
}
```

## Problem 1095A-2

Consider a string of characters of length n and integer k. Divide the string into k-sized chunks. Print the first char of each chunk. 

```
Input
The first line contains n (1 ≤ n ≤ 55) and k (1 ≤ k ≤ 54) -- the length of the string and the chunk size.
The second line contains the string of chars.

Output
Print the first char of every k-sized chunks.

Example

Input
10 3
abcdefghij

Output
adgj

Input
10 4
aaaabbbbcc

Output
abc
```

### Solution Approach

Read a char, skip the next k-1 chars. Repeat this till all n chars are read. Consequently, the chars at positions 1, k+1, 2k+1, .... gets printed.

### Implementation considerations
None

### Implementation
Repeatedly read chars and keep track of the position. Let i denote the position of the char read. If i%k equals 1, then print the char read. 

``` c
// kthchars.c

#include <stdio.h>

int main() {
    int n, k;
    scanf("%d", &n);  // read n
    scanf("%d\n", &k); // read k 
    // Again \n is important, as we are going to read a char next

    char ch;
    int i = 1;
    while (i <= n) {
        scanf("%c", &ch);   // read a char
        if ( i%k == 1)
            printf("%c", ch);
        i++;
    }
    printf("\n"); // a newline
    
    return 0;
}
```

## Problem 1095A-3

Consider a string of characters of length n. Divide the string into k-sized chunks where k takes increasing values starting from 1. Print the first char of each chunk. 

```
Input
The first line contains n (1 ≤ n ≤ 55) -- the length of the string.
The second line contains the string of chars.

Output
Print the first char of every chunk.

Example

Input
10
abcdefghij

Output
abdg

Input
10
abbcccdddd

Output
abc
```

Note:
 - In the first example, the string is divided into chunks a | bc | def | ghij, and therefore the output is abdg.
 - In the second example, the string is divided into chunks a | bb | ccc | dddd, and therefore the output is abcd.

### Solution Approach

Read a char, skip the next k-1 chars. Increment k. Repeat this till all n chars are read. Consequently, the chars at positions 1, 2, 4, 7, .... get printed.

### Implementation considerations
None

### Implementation

 - Initialize k = 1
 - Intialize i = 1.
 - Repeated until the end of the string (i <= n)
 - Read a char and print it (increment i)
 - Read and ignore k - 1 chars (increment i for each read)
 - Increment both k
 
``` c
// varyingk.c

#include <stdio.h>

int main() {
    int n;
    scanf("%d\n", &n); // read n 

    char ch;
    int k = 1;
    int i = 1;
    while (i <= n) {
        scanf("%c", &ch);   // read a char
        printf("%c", ch);   // print the char
        i++;                // increment i

        int j = 1;
        while ( j <= k-1 ) { // Skip next k-1 chars
            scanf("%c", &ch);
            i++;
            j++;
        }
        k++;
    }
    printf("\n"); // a newline
    
    return 0;
}
```

## Submission
 - Check out the problem 1095A Repeating Cipher in [https://codeforces.com/problemset/problem/1095/A](https://codeforces.com/problemset/problem/1095/A)
 - After checking your program thoroughly, submit your solution and get an Accepted message.
