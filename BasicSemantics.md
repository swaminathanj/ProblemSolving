# Semantics of basic C langauge constructs

 - Syntax error = Error in program structure --> Compiler error
 - Semantic error = Error in program meaning --> Compiler error/warning/runtime error 
 - Logical error = Error in program logic --> Compiles, runtime error (unexpected)

## (A) printf

Assumption: x, y are of int types

 1. printf("%d", x)   --> Missing semicolon
                         Syntax error

 2. printf("%d, x")   --> Wrong placement of quotes
                         Syntax error

 3. printf("%f", x);  --> Wrong format specifier
                         Semantic error

 4. printf("%z", x);  --> Invalid format specifier
                         Semantic error

 5. printf("%d %d", x); --> Mismatch in #format specifier
                           Semantic error

 6. printf("x+y = %d", x-y); --> Meant sum, performed difference
                                Logical error

## (B) scanf

Assumption: x, y are of int types
            a, b, c are of char types
            p, q, r is of float type

 1. scanf("%d, &a);   --> Missing end quote
                         Syntax error

 2. scanf("%d", a)    --> Expecting address, got value instead
                         Semantic error

 3. scanf("%c%c%c", &a, &b, &c);  
   Input: 123                
   Effect: a = '1', b = '2', c = '3'

 4. scanf("%c%c%c", &a, &b, &c);
   Input: 1
          2
          3                  
   Effect: a = '1', b = '\n', c = '2'     (Logical error)

 5. scanf("%c\n%c\n%c", &a, &b, &c);
   Input: 1
          2
          3                  
   Effect: a = '1', b = '2', c = '3'      (Correct way to read)

 6. scanf("%c%d", &a, &x);
   Input: 123
   Effect: a = '1', b = 23

 7. scanf("%f", &r);
   Input: 123
   Effect: r = 123.0

 8. scanf("%d", &x);
   Input: 12.3
   Effect: x = 12

 9. scanf("%d%f", &x, &r);
   Input: 12.3
   Effect: x = 12, r = 0.3

 10. scanf("%d.%d", &x, &y);
    Input: 12.3
    Effect: x = 12, y = 3

 11. x = scanf("%d", &x);
    Input = 123;
    Effect: x = 1;
    
## (C) Declaration & assignment

 1. int x 2;       --> Missing '=' operator
                      Syntax error

 2. int x = 2.5;   --> Effect x = 2 (a good compiler will throw error)
                      Semantic error

 3. float r = 2;   --> Valid assignment (Why?)
                      Effect: r = 2.0

 4. int x = 5, y = 2, z;
   z = x/y;              --> Effect: z = 2 (Why not 2.5?)

 5. int x = 5, y = 2;
   float r = x/y;        --> Effect: r = 2 (Why not 2.5 now?)

 6. int x = 5;
   float p = 2.0, r;
   r = x/p;              --> Effect: r = 2.5 (Finally worked)

 7. int x;
   float x;      --> x is already defined
                     Semantic error

 8. int x;
   int y = x/2;  --> x is not initialized, may have a garbage value
                     Logical error

 9. int x = x/2;  --> x is not defined, cyclic dependency
                     Semantic error

 10. char a = 'xy';  --> 'xy' is not a single char
                        Semantic error

 11. char a = 65;    --> Valid assignment (Why?)
    printf("%c ", a);   print a as char and as int and check
    printf("%d ", a);   65 is the ASCII value of 'A'

 12. char a = 128;   --> Invalid assignment (Why?)

 13. char a = 'A';
    a++;            --> Valid increment (Why?)
    printf("%c ", a);   print a as char and as int and check
    printf("%d ", a);   Effect: 'B' is printed

 14. char a = '\n'   
    a++;            --> Valid increment again
                        print and check it out

 15. int x = INT_MAX;
    x++;               --> Effect: x = INT_MIN

 16. int y = INT_MIN;
    y--;               --> Effect: y = INT_MAX

 17. unsigned int x = UINT_MAX;
    y++;               --> Effect: y = 0

## (D) Increment/Decrement operations

 1. int x = 1;
   x++;              Effect: x = 2

 2. int x = 1;
   ++x;              Effect: x = 2

 3. int x = 1;
   int y = x++;  --> First assign, then increment
                     Effect: x = 2, y = 1

 4. int x = 1;  
   int y = ++x;  --> First increment, then assign
                     Effect: x = 2, y = 2

 5. int x = 1;
   int y = 2 * x++;  --> First multiply & assign, then increment
                         Effect: x = 2, y = 2

 6. int x = 1;  
   int y = 2 * ++x;  --> First increment, then multiply and assign
                         Effect: x = 2, y = 4
 

## (E) Control structures

Assumption: x, y, z are of int types

 1. while ( x < y )
      x++;           --> Only x incremented in while loop
      y--;               Logical error

 2. if ( x = y ) {    --> Assign op used instead of ==
        :                Logical error
        :
   }

 3. if ( x < y )
        :
   if ( x > z )
        :
   else              --> else part for which if statement?
        :                (Usually else binds with closest if)

 4. if ( x > y && --x > z )   --> If x <= y, --x may not happen
        :                        (short circuited evaluation)

 5. if ( x > y || --x > z )   --> If x > y, --x may not happen
        :                        (short circuited evaluation)
   
   Bottomline: Never write code with side-effects

 6. if ( x )      
      :          --> This part is executed if x > 0
   else
      :          --> This part is executed if x <= 0

 7. if ( x > y )
      :
   else if ( x > y && y > z )
      :           --> This statement is not reachable
   else               Logical error
      :               

   Suggestion: Put stronger condition before weaker always
           OR 
   alternately implement as below

   if ( x > y ) {
      :           
      if ( y > z )
          :
   }
   else
      :

 8. int i = 1;
   while ( i > 10 ) {  --> While body never entered
     :                     Logical error
     i++;
   }

 9. int i = 1;
   while ( i < 10 ) {  --> Infinite loop since i is not incremented
       :                   Logical error
   }
   
 10. for (int i = 1; i < 10; i++) {
          :
    }
    printf("%d", i);   --> i not defined

 11. int i = 1;
    while ( i < 10) {            for (int i=1; i<10; i++) {
       ::::             SAME AS      ::::
       ::::                      }
       i++;  
    }

 12. do {                            ::::
       ::::                         ::::
       ::::                       while (i < 10) {
       i++;            SAME AS         ::::
    } while (i < 10);                   ::::
                                       i++;
                                  }

 13. for (int i=1; i<10; i++);   --> for loop ends due to semi-colon
    {                               Semantic error
        // This code is executed    (same applies to while loop too)
        // only once
    } 
 14. if ( cond1 ) { ... }                switch(cond) {
   else if ( cond2 ) { ... }  SAME AS  case 1: .....
   else if ( cond3 ) { ... }                   break;
   else { ... }                        case 2: .....
                                               break;
                                       case 3: .....
                                               break;
                                       default: ....
                                       }

 15. if ( cond3 ) {                     switch(cond) {         
      if ( cond2 ) {
          if (cond1) {   SAME AS       case 1: ....
            ....                                    // no break;
          }                            case 2: ....   
          ....                                      // no break;
      }                                case 3: ....
      ....                                          // no break;
    }                                  default: ....
    else {                                  
       ....                            }
    }


## (F) Functions

 1. int func() {
      :
     return x;   // x should be an int
   }

   int main() {
      int x = func(); --> Returns an integer, catch it in variable
      return 0;           (The x in main has nothing to with x in func
   }                       Both are very different)

 2. void func() {      --> Use void if nothing is returned
      :
      return; // not necessary
   }

   int main() {
      func();     --> Doesn't return anything
      return 0;       NOTE: void v = func(); is wrong
   }

 3. void func(int a, int b) {
      :
      return;
   }

   int main() {
      func(2);      --> Formal and actual parameters mismatch
      return 0;         Semantic error
   }

 4. float func(int a, int b) {
      :
      return;
   }

   int main() {
      int x = func(2, 3);   --> func() returns float, but assigned to an int 
      return 0;                 Semantic error
   }

 5. int func(int a, int b) {  --> Return undefined of a >= b
      if (a < b)                 Semantic error
         return a;
   }

 6. int x = 5, y = 10;    --> Global variables
   
   int main() {
      printf("%d %d", x, y);  --> Prints 5 10
      return 0;                   Globals can be accessed
   }                              from the entire file

 7. int x = 5, y = 10;    --> Global variables
   
   int main() {
      int x = 2;              --> Local x hides global x
      printf("%d %d", x, y);  --> Prints 2 10
      return 0;
   }

In addition, you can go through the role of the keywords 'break' and 'continue' in for/while/do-while loops and switch...case from any
C programming book.

## Points to Note 
 - Keep the code simple and readable.
 - Practice breaking the implementation into smaller functions even if your program is small. It is a bad practice to implement everything in main (or a single function).
 - Get your logic straightened by working out on a piece of paper before you start coding. It is more of brainwork than typing work.
 - Don't define unnecessary variables and complicate the code.
 - You don't have to use all the fancy features of language. It is enough if you know them.
 - Don't write large piece of code and compile all at once till you master the syntax. Otherwise, you will be lost in the pool of compilation errors. It will take away your focus from logic.
 - Don't seek help without trying enough yourself. Your confidence will diminish gradually. Moreover, you will endup begging for help forever.
