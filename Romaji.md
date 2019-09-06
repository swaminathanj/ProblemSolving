# Problem 1008A

## Problem 1008A-1

Given a character as input, check if it is a vowel. Print YES if it is so, otherwise NO.

```
Input
A character c which takes a value in the range 'a', ...., 'z'. 

Output
YES if c is a vowel, otherwise NO.

Example

Input
e

Output
YES

Input
u

Output
YES

Input
g

Output
NO
```

### Solution Approach
This is straightforward.

### Implementation considerations
None

### Implementation
Read and check if the char is either 'a', 'e', 'i', 'o' or 'u'. This is implemented by a function isvowel. Print YES or NO accordingly.

``` c
// vowel.c

#include <stdio.h>

int isvowel(char ch) {
    if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
        return 1;
     else
        return 0;
}

int main() {
    char ch;
    scanf("%c", &ch);
    if ( isvowel(ch) )
        printf("YES\n");
    else
        printf("NO\n");

    return 0;
}
```

## Problem 1008A-2

Given a sequence of characters as input, check if every character is a vowel. Print YES if it is so, otherwise NO.

```
Input
A sequence s which every character takes a value in the range 'a', ...., 'z'. 

Output
YES if each character is a vowel, otherwise NO.

Example

Input
aeiou

Output
YES

Input
eeeee

Output
YES

Input
abeioou

Output
NO
```

Note: In the third example, the second char is not a vowel.

### Solution Approach
Read through the sequence of chars, one at a time, check if it is a vowel. Print NO upon encountering the first non-vowel char. Otherwise print YES after the end of the sequence is reached.

### Implementation considerations
Although implementing the loop is straightforward, identifying the end the sequence is not. The exit criteria for the loop should be properly defined. since the size of the sequence is arbitrary and not known. We note that the sequence could be followed by (i) a blank space ' ',  (ii) a tab space '\t' or (iii) a new line '\n'. There is a 4th possibility, that is, end-of-file denoted by a macro EOF. Pressing Ctrl+D produces this char.

### Implementation
Read and check if each char is either 'a', 'e', 'i', 'o' or 'u' until one of the following chars: ' ', '\t', '\n' and EOF is met. This is implemented by the function isend. Print YES or NO accordingly.

``` c
// vowelsequence.c

#include <stdio.h>

int isvowel(char ch) {
    if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
        return 1;
     else
        return 0;
}

int isend(char ch) {
    if (ch == ' ' || ch == '\t' || ch == '\n' || ch == EOF)
        return 1;
    else
        return 0; 
}

int main() {
    char ch;
    scanf("%c", &ch);  // Read a char
    while ( !isend(ch) ) {  // while it not the end char
        if ( isvowel(ch) )  // if it is vowel 
            scanf("%c", &ch);  // read the next char
        else {                 // criteria broken
            printf("NO\n");
            return 0;  // No need to scan the rest
        }
    }
    // We did not find a single consonant char all through
    printf("YES\n");
    return 0;
}
```

## Problem 1008A-3

Given a sequence of characters as input, determine if there are two consecutive consonants.

```
Input
A sequence s which every character takes a value in the range 'a', ...., 'z'. 

Output
Print "NO" if there are two consecutive consonants. Otherwise "YES".

Example

Input
axeyizowu

Output
YES

Input
aeiou

Output
YES

Input
abeicdoou

Output
NO
```

### Solution Approach
Maintain the last two chars. Check if both of them are consonants.

### Implementation considerations
None

### Implementation
Define variables ch and last. For the first time, read the first 2 chars into last and ch respectively. Check if both are consonants. If so, print "NO" and exit. If not, copy ch to last and read the next char into ch. Repeat this till the end of the sequence. Finally print "YES".

``` c
// no2consonants.c

#include <stdio.h>

int isvowel(char ch) {
    if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
        return 1;
     else
        return 0;
}

int isend(char ch) {
    if (ch == ' ' || ch == '\t' || ch == '\n' || ch == EOF)
        return 1;
    else
        return 0; 
}

int main() {
    char ch, last;

    scanf("%c", &last);  // read the first char
    scanf("%c", &ch);    // read the next char 

    while ( !isend(ch) ) {  // while the next char is not the end char
        if ( !isvowel(ch) && !isvowel(last) ) {  // if last 2 chars are consonants
            printf("NO\n"); // no need to scan the rest
            return 0;
        }
        else {
            last = ch;
            scanf("%c", &ch);
        }
    }

    // We did not find a two consecutive consonants all through
    printf("YES\n");
    return 0;
}
```

## Problem 1008A-4

Given a sequence of characters as input, determine if there are two consecutive consonants. Also, the sequence should not end with a consonant.

```
Input
A sequence s which every character takes a value in the range 'a', ...., 'z'. 

Output
Print "NO" if there are two consecutive consonants or the sequence ends with a consonant. Otherwise "YES".

Example

Input
axeyizowu

Output
YES

Input
aeixyou

Output
NO

Input
abeicooud

Output
NO
```

### Solution Approach
Maintain the last two chars. Check if both of them are consonants. Finally, check if the last char of the sequence is a consonant.

### Implementation considerations
None

### Implementation
Define variables ch and last. For the first time, read the first 2 chars into last and ch respectively. Check if both are consonants. If so, print "NO" and exit. If not, copy ch to last and read the next char into ch. Repeat this till the end of the sequence. At the end, check if last holds a consonant. If so, print "NO" and exit. Finally, print "YES".

```
// nolastconsonant.c

#include <stdio.h>

int isvowel(char ch) {
    if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u' || ch == 'n')
        return 1;
     else
        return 0;
}

int isend(char ch) {
    if (ch == ' ' || ch == '\t' || ch == '\n' || ch == EOF)
        return 1;
    else
        return 0; 
}

int main() {
    char ch, last;

    scanf("%c", &last);  // read the first char
    scanf("%c", &ch);    // read the next char 

    while ( !isend(ch) ) {  // while the next char is not the end char
        if ( !isvowel(ch) && !isvowel(last) ) {  // if last 2 chars are consonants
            printf("NO\n"); // no need to scan the rest
            return 0;
        }
        else {
            last = ch;
            scanf("%c", &ch);
        }
    }

    if ( !isvowel(last) ) { // Note: ch now holds end char. last holds the last char of the input sequence
        printf("NO\n");
        return 0;
    }

    // We did not find a two consecutive consonants all through and last char is not a consonant
    printf("YES\n");
    return 0;
}
```

## Problem 1008A-5

Given a sequence of characters as input, determine if there are two consecutive consonants. The sequence should not end with a consonant. The only exception is for the character 'n'. 'n' can be followed by any character vowel or constant. Also, the sequence can end with 'n'.

```
Input
A sequence s which every character takes a value in the range 'a', ...., 'z'. 

Output
Print "NO" if there are two consecutive consonants or the sequence ends with a consonant. Otherwise "YES".

Example

Input
axenyizowu

Output
YES

Input
aeixnyou

Output
NO

Input
abeicooud

Output
NO
```

### Solution Approach
Maintain the last two chars. Check if both of them are consonants. Finally, check if the last char of the sequence is a consonant.

### Implementation considerations
None

### Implementation
Define variables ch and last. For the first time, read the first 2 chars into last and ch respectively. Check if both are consonants. If so, print "NO" and exit. If not, copy ch to last and read the next char into ch. Repeat this till the end of the sequence. At the end, check if last holds a consonant. If so, print "NO" and exit. Finally, print "YES".

``` c
// notwithn.c

#include <stdio.h>

int isvowel(char ch) {
    if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
        return 1;
     else
        return 0;
}

int isend(char ch) {
    if (ch == ' ' || ch == '\t' || ch == '\n' || ch == EOF)
        return 1;
    else
        return 0; 
}

int main() {
    char ch, last;

    scanf("%c", &last);  // read the first char
    scanf("%c", &ch);    // read the next char 

    while ( !isend(ch) ) {  // while the next char is not the end char
        if ( !isvowel(ch) && (!isvowel(last) && last != 'n') ) {  // if last 2 chars are consonants
            printf("NO\n"); // no need to scan the rest
            return 0;
        }
        else {
            last = ch;
            scanf("%c", &ch);
        }
    }
    if ( !isvowel(last) && last != 'n') {
        printf("NO\n"); // no need to scan the rest
        return 0;
    }
       

    // We did not find a two consecutive consonants all through with the exception of 'n'
    printf("YES\n");
    return 0;
}
```

## Submission
 - Check out the problem 1008A Romaji in [https://codeforces.com/problemset/problem/1008/A](https://codeforces.com/problemset/problem/1008/A)
 - After testing your program thoroughly, submit your solution and get an Accepted message.
