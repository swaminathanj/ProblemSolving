This document covers the intermediate syntax and semantics that includes arrays, strings, common library functions, recursion, structures and bitwise operators

## 1. Arrays

### arraydef.c

``` c
/* 
 * A program that defines an integer array and
 * prints the elements of the array
 * Compilation: gcc arraydef.c -o arraydef
 * Execution: ./arraydef
 */

#include <stdio.h>

int main() {
  int arr[5] = {-3, 11, -26, 48, 31};
  for (int i=0; i<5; i++)
    printf("%d", arr[i]);

  return 0;
}
```

#### Semantics

 - The size of the array is mentioned within square brackets. The number of elements on the RHS should match the size.
 - You can drop the size within the square bracket. It will automatically calculate the size based on the number of elements in RHS.
 - arr represents the array itself whereas arr[i] denotes the ith element.
 - arr[0] contains the first element (-3). arr[4] contains the fifth/last element (31). The indexing starts from 0.
 - A single element of an array can be accessed by the array name and the index. i.e. a[i] where 0 ≤ i < 5.
 - Each element is an integer (in this case). Hence, %d is used as the format specifier.

### arraydecl.c

``` c
/* 
 * A program that declares an integer array and
 * reads the elements of the array from stdin
 * Compilation: gcc arraydecl.c -o arraydecl
 * Execution: ./arraydecl
 */

#include <stdio.h>

int main() {
  int arr[5];
  for (int i=0; i<5; i++)
    scanf("%d", &arr[i]);

  return 0;
}
```

#### Semantics
 - You can declare the array and then populate it by reading the elements from terminal.
 - In this case, it is necessary to mention the size of the array within the square brackets.
 - Each element is of type int (in this case) and hence %d is used as format specifier.
 - Declaration of arrays of other types - char, short, long, float, double - are analogous.

### arraysize.c

``` c
/* 
 * A program that declares an integer array of
 * variable size and reads the elements from stdin
 * Compilation: gcc arraysize.c -o arraysize
 * Execution: ./arraysize
 */

#include <stdio.h>

int main() {
  int n;
  scanf("%d", &n);
  int arr[n];
  for (int i=0; i<n; i++)
    scanf("%d", &arr[i]);

  return 0;
}
```

#### Semantics
 - You can declare array of any size and then populate it by reading the elements from terminal.
 - First take size (n) of the array as input and declare an array of that size.
 
### arrayops.c

``` c
/* 
 * A program that demonstrates operations
 * on arrays
 * Compilation: gcc arrayops.c -o arrayops
 * Execution: ./arrayops
 */

#include <stdio.h>

int main() {
  int n;
  scanf("%d", &n);
  int arr[n];
  for (int i=0; i<n; i++)
    scanf("%d", &arr[i]);

    int x = arr[2] * arr[3] / arr[4];
    int y = arr[0] + arr[1] - x;
    if ( arr[2] < arr[3] && arr[4] == 100 )
      printf("Condition satisfied");

  return 0;
}
```

#### Semantics
 - You can operate on individual elements as you do on primitive types.
 - All operations - arithmetic, comparison and logical - can be performed on array elements.
 
### arraymax.c

``` c
/* 
 * A program that passes an array as a parameter
 * to a function to determine the max element 
 * Compilation: gcc arraymax.c -o arraymax
 * Execution: ./arraymax
 */

#include <stdio.h>

int findmax(int a[ ], int size) { // function definition
  int max = a[0];
  for (int i=1; i<size; i++) {
    if ( a[i] > max )
      max = a[i];
  }
  return max;
}

int main() {
  int n;
  scanf("%d", &n);
  int arr[n];
  for (int i=0; i<5; i++)
    scanf("%d", &arr[i]);

    int max = findmax(arr, n); // function call
    printf("%d", max));

  return 0;
}
```

#### Semantics
 - To pass an array to a function, define it with two parameters, one for array and another size. This makes it flexible.
 - While making the function call, pass the array name (here arr) and the size (here n).
 - Returning an array is not possible. Luckily you don't have to. For practical purposes, passing an array to the function being called is sufficient.

Let's say function main() declares an array a[] and calls a function increment() passing a and its size.
 - The increment() function increases the value of each element of a by 10
 - After the increment() completes, changes made to array a is accessible from main().
 - In other words, increment() need not have to return the modified array back to the main. The following example illustrates.

### arrayret.c

``` c
#include <stdio.h>

void increment(int a[], int size) {  // This function gets array from its caller and
    for (int i=0; i<size; i++)            //  does not return back the modified array
        a[i] += 10;
}

int main() {
    int a[] = {1, 2, 3, 4};
    increment(a, 4);        // However after increment returns, a has modified values
    for (int i=0; i<4; i++)
        printf("%d ", a[i]);   // prints 11 12 13 14

    return 0;
}
```

### Practice problems (break your implementation into functions)

```
1. UNIQUE: Given an array, you have to determine if all the elements of the array are unique. If so, it should print YES. Otherwise print NO. {28, 61, -14, 7, 44, -35, 50} has unique elements whereas {28, 61, -14, 7, 44, -35, 44} does not.
Input: In the first line a single integer n that denotes the size of the array. The second line contains n integers.
Output: YES or NO
2. PEAK ELEMENT: Given a bitonic array, you have to determine the peak element. A bitonic array is an array which contains elements that is initially increasing and then decreasing. { -17, -3, 4 , 12, 38, 26, 9, 0, -1} is a bitonic array and the peak element is 38.
Input: In the first line a single integer n that denotes the size of the array. The second line contains n integers.
Output: A single integer that is the peak
3. ROTATION: Rotate an array k times. For example, rotating the array {1, 2, 3, 4, 5, 6, 7, 8} by k = 3 times results in the array {4, 5, 6, 7, 1, 2, 3}.
Input: The first line contains two integers n and k. The second line contains n integers.
Output: Print the rotated array.
4. MERGE: Given two sorted arrays, you have to merge them both into a single sorted array. For example, merging {1, 3, 6, 7} and {2, 4, 5, 8} results in {1, 2, 3, 4, 5, 6, 7, 8}.
Input: The first line contains the sizes of two input arrays n and m. The second line contains n elements of the first sorted array. The third line contains m elements of the second sorted array.
Output: Elements of the merged sorted array
```

## 2. Strings
Strings are one-dimensional array of chars terminated by the null character '\0'. Why do we need the null character? Simply because all words are not of the same size. If in the problem being dealt, all words are guaranteed to be of same size, then char array is sufficient. If not, use strings. The purpose of null char is to figure out that the word actually ended. In short, a string is a variable sized char array with '\0' to signify the end. 

Strings are written within double quotes. For example, "hello" is a string and is equivalent to char array {'h', 'e', 'l', 'l', 'o', '\0'}.

### stringdef.c

``` c
/* 
 * A program that defines a string and
 * prints it
 * Compilation: gcc stringdef.c -o stringdef
 * Execution: ./stringdef
 */

#include <stdio.h>

int main() {
  char str[] = "hello"; // same as {'h', 'e', 'l', 'l', 'o', '\0'}
  printf("%s", str);

  return 0;
}
```

#### Semantics
 - The size of the string is 6. It automatically places '\0' at the end and counts it.
 - str represents the string itself whereas str[i] denotes the ith char.
 - str[0] contains the first char ('h'). str[5] contains the sixth/last char ('\0'). The indexing starts from 0.
 - A single element of the string can be accessed by the array name and the index. i.e. str[i] where 0 ≤ i < 6.
 - The string can be printed as a whole using the format specifier %s. To print a single char, %c is used.
 
### stringdecl.c

``` c
/* 
 * A program that declares a string variable
 * and reads it from stdin
 * Compilation: gcc stringdecl.c -o stringdecl
 * Execution: ./stringdecl
 */

#include <stdio.h>

int main() {
  char name[20];
  scanf("%s", name);

  return 0;
}
```

#### Semantics
 - You can declare a string variable and then populate it by reading the string at one shot from terminal.
 - The string can be read at one shot using %s as format specifier.
 - The size of the string is 20, but its length can be at most 20 depending on the number of chars.

### stringops.c

``` c
/* 
 * A program that demonstrates operations
 * on strings
 * Compilation: gcc stringops.c -o stringops
 * Execution: ./stringops
 */

#include <stdio.h>

int main() {
  char word[10];
  scanf("%s", word);

  for (int i=0; word[i] != '$' || word[i] != '\0'; i++)
      printf("%c", word[i]);  // Read until $ or end of string

  return 0;
}
```

#### Semantics
 - Strings can be worked with like char arrays. Only caution is to not go beyond '\0' char while doing so.
 - As far as C strings are concerned, length and size are different.
 - All operations -  comparison and logical - can be performed on individual chars.
 - Any arithmetic operation done on individual chars will be on their ASCII values.
 
## 3. Two dimensional arrays

### array2d.c

``` c
/* 
 * A program that demonstrates working 
 * with two-dimensional arrays (matrix).
 * Compilation: gcc array2d.c -o array2d
 * Execution: ./array2d
 */

#include <stdio.h>
#include <limits.h>

int findmax(int a[ ], int size) { // function definition
  int max = a[0];
  for (int i=1; i<size; i++) {
    if ( a[i] > max )
      max = a[i];
  }
  return max;
}

int findmax2d(int a[][], int rows, int cols) { // function definition
  int max = INT_MIN;
  for (int i=0; i<rows; i++) {
     int rowmax = findmax(a[i], cols); // a[i] is ith row
     if ( rowmax > max )
       max = rowmax;
  }
  return max;   
}

int main() {
  int n, m;     // n rows with m columns
  scanf("%d %d", &n, &m);
  int arr[n][m];

  for (int i=0; i<n; i++) {
    for (int j=0; j<m; j++)
      scanf("%d", &arr[i][j]);
  }

  printf("%d", findmax2d(arr, n, m));  
  return 0;
}
```

#### Semantics
 - arr[i][j] denotes the element in ith row and jth column.
 - arr[i] denotes the ith row.
 - arr denotes the array itself.

4. Recursion
 

5. Bitwise Operators
For the purpose of demonstration, 8 bit representation for the numbers is assumed.

Binary AND operator: &
Copies a bit to the result if it exists in both operands.
r = 13 & 6; // r gets the value of 4
0 0 0 0 1 1 0 1
0 0 0 0 0 1 1 0  &
---------------
0 0 0 0 0 1 0 0   =   4
---------------
Application: & can be used (i) to determine the bit at kth position and (ii) to set the kth bit to 0.
k = 0 denotes the rightmost bit position.
k = 7 denotes the leftmost bit position (in this demonstration).
Note: For 32-bit integer, leftmost bit position is 31. for 64-bit long, leftmost bit position is 63.

Problem 1: Let's say we want to know the bit at position k for the number n.  
Solution: To determine this, all you have to do is to perform a binary AND operation of n with 2k i.e. 8. Assuming you have function power(int x, int y) to compute xy, which you can invoke by passing 2 and k to get 2k, you can accomplish it by the following check:
- If ( n & power(2,k) == power(2,k) ) then 1 is present in kth position of n.
- If ( n & power(2,k) == 0 ) then 0 is present in kth position of n.
Example 1: n = 13, k = 3
0 0 0 0 1 1 0 1         (n = 13)
0 0 0 0 1 0 0 0   &   (k = 3 ==> 2k = 8)
---------------
0 0 0 0 1 0 0 0  =  8 
---------------
Example 2: n = 13, k = 6
0 0 0 0 1 1 0 1         (n = 13)
0 1 0 0 0 0 0 0   &   (k = 6 ==> 2k = 64)
---------------
0 0 0 0 0 0 0 0  =  0
---------------
Problem 2: How to set the kth bit to 0?
Solution: Left as an exercise
 
Binary OR operator: |
Copies a bit to the result if it exists in at least one operand.
r = 13 | 6; // r gets the value of 15
0 0 0 0 1 1 0 1
0 0 0 0 0 1 1 0  &
--------------
0 0 0 0 1 1 1 1   =   15
--------------
Application: | can be used to set the bit at kth position to 1. 
Problem: How to set the kth bit to 1? 
Solution: Left as an exercise 
 
Binary XOR operator: ^
Copies a bit to the result if it exists in exactly one operand.
r = 13 ^ 6; // r gets the value of 11
0 0 0 0 1 1 0 1
0 0 0 0 0 1 1 0  &
--------------
0 0 0 0 1 0 1 1   =   11
--------------
Application: | can be used to flip the bit at kth position i.e. from 0 to 1 or vice-versa. 
Problem: How to flip the kth bit to 1? 
Solution: Left as an exercise 
 
Binary left shift operator: <<
The left operands value is moved left by the number of bits specified by the right operand.
r = 13 << 5; // r gets the value of 160
0 0 0 0 1 1 0 1  -->  1 0 1 0 0 0 0 0 = 160
Application: << can be used to produce the effect of multiplication. Left shift by 1 implies doubling the value. Left shift by 2 implies doubling twice. Left shift by 10 implies doubling 10 times.
Problem: How do you compute 13 x 7 using << operator?
Solution: This can be done in a sequence of steps.
13 x 5 is same as 0 0 0 0 1 1 0 1 x 0 0 0 0 0 1 1 1
This can be broken down into:
(0 0 0 0 1 1 0 1 x 0 0 0 0 0 0 0 1) + (0 0 0 0 1 1 0 1 x 0 0 0 0 0 0 1 0) + (0 0 0 0 1 1 0 1 x 0 0 0 0 0 1 0 0)
Binary right shift operator: >>
The left operands value is moved right by the number of bits specified by the right operand.
r = 13 >> 2; // r gets the value of 
0 0 0 0 1 1 0 1  -->  0 0 0 0 0 0 1 1 = 3
 
One's complement operator: ~
 
6. Structures
