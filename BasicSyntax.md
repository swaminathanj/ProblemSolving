# Basic Syntax and Semantics of C

## 1. Getting started

### nothing.c

``` c
/* 
 * A program that does nothing
 * Compilation: gcc nothing.c -o nothing
 * Execution: ./nothing
 */

int main() {

  return 0;
}
```

#### Semantics

This is probably the first program you will write. Although it doesn't do anything, it gives a fair idea about the structure of a C program.

 - main is a function that denotes the starting point. (What is a function??)
 - The C runtime system hands over the control to the main when the program is executed.
 - main returns an integer. Generally, 0 is returned if the program executed fine (what is fine??).


## 2. Output

### hello.c

``` c
/* 
 * A program that prints Hello World
 * Compilation: gcc hello.c -o hello
 * Execution: ./hello
 */

#include <stdio.h>

int main() {
    printf("Hello World");
    return 0;
}
```

#### Semantics

 - printf() is a function which is used to write to the terminal. This is defined in the header file stdio.h (what is header??) and hence we have to include the header if we need to use it.

### hello_nl.c

``` c
/* 
 * A program that prints Hello World followed by a newline
 * Compilation: gcc hello_nl.c -o hello_nl
 * Execution: ./hello_nl
 */

#include <stdio.h>

int main() {
    printf("Hello World\n");
    return 0;
}
```

#### Semantics

 - \n denotes the new line character. The backslash '\' before 'n' signifies how 'n' should be interpreted as newline.

### hello_tab.c

``` c
/* 
 * A program that prints Hello World after a tab space
 * Compilation: gcc hello_tab.c -o hello_tab
 * Execution: ./hello_tab
 */

#include <stdio.h>

int main() {
    printf("\tHello World\n");
    return 0;
}
```

#### Semantics

 - \t denotes tab space character. Generally 4 or 8 white spaces.

## 3. Variables and Data types

### char.c

``` c
/* 
 * A program that declares a variable of char type
 * prints it in a formatted way.
 * Compilation: gcc char.c -o char
 * Execution: ./char
 */

#include <stdio.h>

int main() {
  char ch = 'A'; // Variable c holds a character 'A'
  printf("The value of c is %c\n", ch);

  ch = '$';
  printf("ch now holds %c\n", ch);

  return 0;
}
```

#### Semantics

 - A char variable occupies 1 byte/8 bits of memory.
 - A char variable takes ASCII values. i.e. all those you typically see on the keyboard. It includes '0', ..., '9', 'A', ..., 'Z', 'a', ..., 'z', '!', ..., ')', ...
 - A char value has to be specified within single quotes (to distinguish from variable name).

### integer.c

``` c
/* 
 * A program that declares a variable of int type
 * prints it in a formatted way.
 * Compilation: gcc integer.c -o integer
 * Execution: ./integer
 */

#include <stdio.h>

int main() {

  int num = -50;
  unsigned int unum = 100;
  printf("The value of num is %d\t", num);
  printf("The value of unum is %u\t", unum);

  return 0;
}
```

#### Semantics

 - An int variable occupies 4 bytes/32 bits of memory.
 - An int variable takes values in the range -231 and 231 - 1 (-2147483648 to 2147483647).
 - An unsigned int takes values in the range 0 and 232 - 1 (0 to 4294967295).
 - Try assiging a value that is beyond the specified range and see what happens?
 - It can be hard to remember the max and min values. Luckily, you don't have to.

### max_int.c

``` c
/* 
 * A program that prints max value of int type
 * Compilation: gcc max_int.c -o max_int
 * Execution: ./max_int
 */

#include <stdio.h>
#include <limits.h>

int main() {

  printf("The max value an int variable can hold is %d", INT_MAX);
  printf("The max value an unsigned int variable can hold is %u\t", UINT_MAX);

  return 0;
}
```

#### Semantics

 - You can very well guess how to print min values of both.
 - You need to include limits.h in order to use them.
 - There are shorter and longer versions of int type: short (2 bytes/16 bits) and long (8 bytes/64 bits).

### short_long.c

``` c
/* 
 * A program that declares variables of short and long types
 * prints them in a formatted way.
 * Compilation: gcc short_long.c -o short_long
 * Execution: ./short_long
 */

#include <stdio.h>

int main() {

  short sh = -50;
  unsigned short ush = 100;
  printf("The value of s is %d\t", sh);
  printf("The value of us is %u\n", ush);

  long ln = 425;
  unsigned long uln = 109385;
  printf("The value of l is %ld\t", ln);
  printf("The value of ul is %lu\n",uln);

  return 0;
}
```

#### Semantics

 - An short variable takes values in the range -215 and 215 - 1 (-32768 to 32767).
 - An unsigned short takes values in the range 0 and 216 - 1 (0 to 65535).
 - An long variable takes values in the range -263 and 263 - 1 (-9223372036854775808 to 9223372036854775807) on 64 bit systems. On 32 bit systems you have to use long long instead of long. The format specifier is %lld.
 - An unsigned long takes values in the range 0 and 263 - 1 (0 to 18446744073709551615) on 64 bit systems. On 32 bit systems, you have to use unsigned long long instead of unsigned long. The format specifier is %llu.
 - The max values of signed and unsigned versions of short and long are SHRT_MAX, USHRT_MAX, LONG_MAX and ULONG_MAX.
 - Floating point types deal with decimal numbers. There are two variants float and double that occupy 32 bits and 64 bits respectively.

### fptypes.c

``` c
/* 
 * A program that declares variables of floating point types,
 * assigns values and prints them in a formatted way.
 * Compilation: gcc fptypes.c -o fptypes
 * Execution: ./fptypes
 */

#include <stdio.h>

int main() {

  float flt = 25.67;
  printf("The value of f is %f\t", flt);

  double dbl = 45.0000008;
  printf("The value of d is %lf\n", dbl);

  return 0;
}
```

#### Semantics

 - Floating point types are stored as [mantissa, exponent] form.
 - There is not unsigned variant of floating point types.
 - FP variables are stored and manipulated differently.
 - A variable (of any type) can be qualified by a keyword const in order to restrict its modifiable status.

### constant.c

``` c
/* 
 * A program that declares a const value and therefore cannot
 * be modified.
 * Compilation: gcc constant.c -o constant
 * Execution: ./constant
 */

#include <stdio.h>

int main() {

  const float pi = 3.14;
  printf("The value of pi is %f\t", pi);

  // Try uncommenting the below statment and  see if it compiles.
  // pi = 10.1;

  return 0;
}
```

#### Semantics
 - The value of a variable of const type cannot be modified. 

## 3. Input

### input.c

``` c
/* 
 * A program that reads values of variables from keyboard and
 * prints them in a formatted way.
 * Compilation: gcc input.c -o input
 * Execution: ./input
 */

#include <stdio.h>

int main() {
  char ch;
  unsigned long ln;
  float fl;

  printf("Input a char value");
  scanf("%c", &ch);

  printf("Input am unsighed long value");
  scanf("%lu", &ln);

  printf("Input a float value");
  scanf("%f", &fl);

  printf("The values entered are %c, %ul and %f.\n", ch, ln, fl);
  return 0;
}
```

#### Semantics

 - Observe the & in front of the variable names in the scanf(). It refers to the location/address of the variables. &ch, &ln and &fl denote the address of the variables ch, ln and fl respectively. Essentially, it means copy the value to the location of the variable.
 
## 4. Operators

### arithmetic_ops.c

``` c
/* 
 * A program that performs basic arithmetic operations such as
 * addition, substraction, multiplication and division.
 * Compilation: gcc arithmetic_ops.c -o arithmetic_ops
 * Execution: ./arithmetic_ops
 */

#include <stdio.h>

int main() {
  int a, b;
  int sum, diff, product, quotient, reminder;

  scanf("%d", &a);
  scanf("%d", &b);

  sum = a + b;
  diff = a - b;
  product = a * b;
  quotient = a / b;
  remainder = a % b;

  printf("sum = %d\n", sum);
  printf("diff = %d\n", diff);
  printf("product = %d\n", product);
  printf("quotient = %d\n", quotient);
  printf("remainder = %d\n", remainder);

  return 0;
}
```

#### Semantics
 - If the computed values go out of range defined for that type, it will lead to overflow.

### relational_ops.c

``` c
/* 
 * A program that performs relational operations such as equal to, not equal to, 
 * greater than [or equal] to and less than [or equal] to.
 * Compilation: gcc relational_ops.c -o relational_ops
 * Execution: ./relational_ops
 */

#include <stdio.h>

int main() {
  int a, b;

  scanf("%d", &a);
  scanf("%d", &b);

  printf("%d\n", a < b);  // prints 1 if a < b, 0 otherwise
  printf("%d\n", a <= b); // prints 1 if a ≤ b, 0 otherwise
  printf("%d\n", a > b);  // prints 1 if a > b, 0 otherwise
  printf("%d\n", a >= b); // prints 1 if a ≥ b, 0 otherwise
  printf("%d\n", a == b); // prints 1 if a = b, 0 otherwise
  printf("%d\n", a != b); // prints 1 if a ≠ b, 0 otherwise

  return 0;
}
```

#### Semantics

 - If the comparison turn out to be true, result is 1. If not, result is 0.
 - Relational operators are primarily used in evaluating an expression and deciding which path (among two or more) to take based on the result of the evaluation.
 
 
### logical_ops.c

``` c
/* 
 * A program that performs logical operations such as AND, OR and NOT.
 * Compilation: gcc logical_ops.c -o logical_ops
 * Execution: ./logical_ops
 */

#include <stdio.h>

int main() {
  int a, b, c;

  scanf("%d", &a);
  scanf("%d", &b);
  scanf("%d", &c);

  printf("%d\n", a < b && a < c); // prints 1 if a < {b and c}, 0 otherwise
  printf("%d\n", a < b || a < c); // prints 1 if a is < {b or c}, 0 otherwise
  printf("%d\n", !(a > b) );      // prints 1 if a ≤ b, 0 otherwise

  return 0;
}
```

#### Semantics

Logical operators are used to combine multiple relational operations to form a complex or larger evaluation condition.
 - && is AND operator
 - || is OR operator
 - ! is NOT operator
 
## 5. Functions
Functions are independent modules that implement a functionality. They help to keep the code modular by splitting the code into smaller, manageable and reusable units. Function divides the implementation concerns into two parts.

 1. Function definition - Solely concerned about the implementation of the functionality.
 2. Function invocation - Solely concerned about the use of defined function towards the goal.

### square_of_sum.c

``` c
/* 
 * A program that implements a function that computes square of sum.
 * i.e. given two numbers a and b, it computes (a + b)2.
 * Compilation: gcc square_of_sum.c -o square_of_sum
 * Execution: ./square_of_sum
 */

#include <stdio.h>

// This function defines computation of square of sum.
// Here, x and y are referred to as formal parameters.
int square_of_sum(int x, int y) {
  int ss = (x + y) * (x + y);
  return ss;
}

int main() {
  int a, b;

  scanf("%d", &a);
  scanf("%d", &b);

  // Function call to square_of_sum made. a and b are actual parameters.
  int ss = square_of_sum(a, b);

  printf("%d", ss);

  return 0;
}
```

#### Semantics

 - The function square_of_sum takes 2 integer parameters, computes and returns an integer.
 - The main function merely reads the input, delegates the computation to square_of_sum, recieves the result and prints.
 - The variable ss in square_of_sum is different from the variable ss in main, although both have same names. They are local to their respective functions.

Write a program that defines a function sum_of_squares that takes parameters a and b, and computes a^2 + b^2.

### sum_of_squares.c

``` c
/* 
 * A program that implements a function that computes sum of squares.
 * i.e. given two numbers a and b, it computes (a + b)^2.
 * Compilation: gcc sum_of_squares.c -o sum_of_squares
 * Execution: ./sum_of_squares
 */

#include <stdio.h>

int sum_of_squares(int x, int y) {
 
    // Write your code here
}

int main() {

  int ss = sum_of_squares(3,4);

  printf("%d", ss);

  return 0;
}
```

#### Semantics
 - The two statements can be replaced by a single statement: printf("%d", sum_of_squares(3,4));

## 6. Branching

### if.c

``` c
/* 
 * A program that evaluates a condition and performs an
 * action if it is true.
 * Compilation: gcc if.c -o if
 * Execution: ./if
 */

#include <stdio.h>

void is_same(int a, int b) {
  if (a == b) {
    printf("%d is same as %d\n", a, b);
  }
}

int main() {
  int a, b;

  scanf("%a", &a);
  scanf("%b", &b);

  is_same(a, b);

  return 0;
}
```

### if_else.c

``` c
/* 
 * A program that evaluates a condition and decides 
  *different courses of action based on the result.
 * Compilation: gcc if_else.c -o if_else
 * Execution: ./if_else
 */

#include <stdio.h>

void check(int a, int b) {
  if (a == b) {
    printf("%d is same as %d", a, b); // one course of action
  }
  else {
    printf("%d and %d are different\n", a, b); // another course of action
  }
}

int main() {
  int a, b;

  scanf("%a", &a);
  scanf("%b", &b);

  check(a, b);

  return 0;
}
```

Now, lets implement a bit more complex condition. We will check if a given 3 numbers a, b, c form a pythogorean triplet. i.e. a^2 + b^2 equals c^2. We can re-use the previously defined function sum_of_squares.

### pt.c

``` c
/* 
 * A program that checks if 3 numbers a, b, c form a 
 * pythogrean triplet and print Y or N.
 * Compilation: gcc pt.c -o pt
 * Execution: ./pt
 */

#include <stdio.h>

int sum_of_squares(int x, int y) {
  int ss = x*x + y*y;
  return ss;
}

char is_py_triplet(int a, int b) {
  if ( square_of_sum(a, b) == c*c ) {
    return 'Y';
  }
  else {
    return 'N';
  }
}

int main() {
  int a, b, c;

  scanf("%d", &a);
  scanf("%d", &b);
  scanf("%d", &c);

  printf("%c", is_py_triplet(a, b, c)); // is_py_triplet returns a char

  return 0;
}
```

#### Semantics
 - if ( (a*a + b*b) = c*c) ... will work equally well. However, we don't want to reinvent the wheel. Using the function that is tried and tested is better than re-implementing.
  - The implementation of is_py_triplet is not foolproof. It will work correctly only if the last number entered c is largest. What if someone entered 3 5 4? Can you make the condition strong enough to work correctly regardless of the order in which user enters the numbers? (HINT: use logical operators)
  
You can have nested if..else blocks to implement nested branching. An example that sorts 3 numbers is given below.

### nested_ifs.c

``` c
/* 
 * A program that orders 3 distinct numbers a, b, c  
 * in increasing fashion.
 * Compilation: gcc nested_ifs.c -o nested_ifs
 * Execution: ./nested_ifs
 */

#include <stdio.h>

int min, mid, max;    // global variables - accessible from all functions

void sort_3_nums(int x, int y, int z) {

  if (x < y) {                // z could be < x, between x & y or > y
    if (y < z) {             // implies x < y < z
      min = x; mid = y; max = z;
    }
    else {                 // z could be < x or between x & y
      if (x < z) {             // implies x < z < y
        min = x; mid = z; max = y;         
      }
      else {                // implies z < x < y
        min = z; mid = x; max = y;
      }
    }
  }
  else {                 // z could be < y, between y & x, or > x

                    // Write your code and complete

  }
}

int main() {
  int a, b, c;

  scanf("%d", a);
  scanf("%d", b);
  scanf("%d", c);

  sort_3_nums(a, b, c);

  printf("%d < %d < %d", min, mid, max);
}
```

## 7. Loops
Sometimes one may want to repeat an operation several times. This can be accomplished by loop constructs: while, for and do..while.

### while.c

``` c
/* 
 * A program that prints Hello 10 times
 * Compilation: gcc while.c -o while.c
 * Execution: ./while
 */

#include <stdio.h>

int main() {
  int i = 0;                // initial value
  while (i < 10) {            // loop entry condition
    printf("Hello %d", i);
    i++;                // increment operation that tracks count
  }
}
```

### whilen.c

``` c
/* 
 * A program that prints Hello n times
 * Compilation: gcc whilen.c -o whilen.c
 * Execution: ./whilen
 */

#include <stdio.h>

int main() {
  int n;
  scanf("%d", &n);

  int i = 0;
  while (i < n) {
    printf("Hello %d", i);
    i++;
  }
}
```

### while100.c

``` c
/* 
 * A program that reads a number from keyboard
 * until user enters 100
 * Compilation: gcc while100.c -o while100.c
 * Execution: ./while100
 */

#include <stdio.h>

int main() {
  int n;
  scanf("%d", &n);

  while (n != 100) {
    printf("You entered %d, repeat again", n);
    scanf("%d", &n);
  }
  printf("Out of the loop at last!");
}
```

### whilen100.c

``` c
/* 
 * A program that reads a number from keyboard
 * until user enters 100 or for n times.
 * Compilation: gcc whilen100.c -o whilen100.c
 * Execution: ./whilen100
 */

#include <stdio.h>

int main() {
  int n;
  scanf("%d", &n);

  int i = 0;
  while (n != 100 || i < n) {
    scanf("%d", &n);
    i++;
  }
  printf("Out of the loop! n = %d and i = %d", n, i);
}
```
