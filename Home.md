
# Problem Solving using Programming

## Unit 1

### Basic Programming Constructs
 - [Basic Syntax](BasicSyntax.md)
 - [Under the hood: How does a program run?](ProgramExecution.mp4)
 
### Worked out Examples
Problems for which solutions are worked out in an incremental fashion
 1. [Frog Jumping](FrogJumping.md)
 2. [The Rank](TheRank.md)
 3. [Romaji](Romaji.md)
 4. [Ehab and Another Construction](Ehab.md)
 5. [Repeating Cipher](RepeatingCipher.md)

### Problems from Code Forces
Start solving these problems in the lines demonstrated above.
 1. [Golden Plate (1031A)](https://codeforces.com/problemset/problem/1031/A)
 2. [In search of Easy problem (1030A)](https://codeforces.com/problemset/problem/1030/A)
 3. [Integer sequence dividing (1102A)](https://codeforces.com/problemset/problem/1102/A)
 4. [Find Divisible (1096A)](https://codeforces.com/problemset/problem/1096/A)
 5. [Dice Rolling (1093A)](https://codeforces.com/problemset/problem/1093/A)
 6. [Definite Game (1081A)](https://codeforces.com/problemset/problem/1081/A)
 7. [Vova and Train (1066A)](https://codeforces.com/problemset/problem/1066/A)
 8. [Gennady and Card Game (1097A)](https://codeforces.com/problemset/problem/1097/A)
 9. [Uniform String (1092A)](https://codeforces.com/problemset/problem/1092/A)
 10. [Petya and Origami (1080A)](https://codeforces.com/problemset/problem/1080/A)
 11. [The King's Race (1075A)](https://codeforces.com/problemset/problem/1075/A)
 12. [Vasya and Chocolate (1065A)](https://codeforces.com/problemset/problem/1065/A)
 13. [Make a Triangle (1064A)](https://codeforces.com/problemset/problem/1064/A)
 14. [Coins (1061A)](https://codeforces.com/problemset/problem/1061/A)
 15. [Sum of digits (FLOW006)](https://www.codechef.com/problems/FLOW006)
 16. [Bear and Big Brother (791A)](https://codeforces.com/problemset/problem/791/A)
 
### A recap
 - [Semantics of Basic Syntax Constructs](BasicSemantics.md)
 - [Basic Programming Patterns](ProgrammingPatterns.md)

## Unit 2

### Intermediate Programming constructs
 - [Intermediate Syntax](IntermediateSyntax.md)
 
### Problems from Code Forces
#### Arrays
 1. [Array Stabilization (1095B)](http://codeforces.com/problemset/problem/1095/B)
 2. [Good Number (365A)](http://codeforces.com/problemset/problem/365/A)
 3. [Mishka and Contest (999A)](https://codeforces.com/contest/999/problem/A)
 4. [Ehab and Subtraction (1088B)](http://codeforces.com/problemset/problem/1088/B)
 5. [Polycorp's Pockets (1003A)](https://codeforces.com/problemset/problem/1003/A)
 6. [Less or Equal (977C)](http://codeforces.com/problemset/problem/977/C)
 7. [Songs Compression (1015C)](http://codeforces.com/problemset/problem/1015/C)
 8. [Planning Expedition (1011B)](http://codeforces.com/problemset/problem/1011/B)
 9. [Unimodal Array (831A)](http://codeforces.com/problemset/problem/831/A)
 
#### Strings
 1. [Mike and Palindrome (798A)](https://codeforces.com/contest/798/problem/A)
 2. [Superhero Transformation (1111A)](http://codeforces.com/problemset/problem/1111/A)
 3. [Right-Left Cipher (1085A)](http://codeforces.com/problemset/problem/1085/A)
 4. [Minimize the String (1076A)](http://codeforces.com/problemset/problem/1076/A)
 5. [Palindromic Twist (1027A)](http://codeforces.com/problemset/problem/1027/A)
 6. [Letters Rearranging (1093B)](http://codeforces.com/problemset/problem/1093/B)
 7. [Delete from Left (1005B)](http://codeforces.com/problemset/problem/1005/B)
 8. [Antipalindrome (981A)](http://codeforces.com/problemset/problem/981/A)
 9. [File Name (978B)](http://codeforces.com/problemset/problem/978/B)
 10. [Two-gram (977B)](http://codeforces.com/problemset/problem/977/B)

#### Problems on Bitwise operators

 1. Find the bit at kth position of n's binary representation.
```
  Input: n, k
  Output: 1 if 1 was present at kth position. 0 otherwise.
  Sample 1:  1 0        ==> 1
  Sample 2: 21 4        ==> 1
  Sample 3: 21 3        ==> 0
  Sample 4: 3972947 7   ==> 0
  Sample 5: 3972947 20  ==> 1
 ```
 
 2. Find if an integer n is negative? i.e. Is leftmost digit set to 1?
```
  Input: n
  Output: YES if n is negative. NO otherwise.
  Sample 1: -1         ==> YES
  Sample 2: 21         ==> NO
  Sample 3: -3972947   ==> YES
  Sample 4: 2147483648  ==> YES //  INT_MAX+1 leads to overflow
  Sample 5: -2147483649  ==> NO  // INT_MIN-1 leads to underflow
```

 3. Set the bit at kth position of n's binary representation to 1.
```
Input: n, k
  Output: Resulting number after kth bit is made 1
  Sample 1:  1 0        ==> 0
  Sample 2: 21 3        ==> 21
  Sample 3: 3972947 20  ==> 1 
 ```
 
 4. Set the bit at kth position of n's binary representation to 0.
```
  Input: n, k
  Output: Resulting number after kth bit is made 0
  Sample 1:  1 0        ==> 0
  Sample 2: 21 3        ==> 21
  Sample 3: 3972947 20  ==> 1   
 ```

 5.  Count the number of 1's in binary representation of n.
 
```
  Input: n
  Output: number of 1's
  Sample 1:  0         ==> 0
  Sample 2: 21         ==> 3
  Sample 3: 2147483647    ==> 31  //  INT_MAX
  Sample 4: 2147483648  ==> 1   //  INT_MAX+1 leads to overflow
  Sample 5: 1024       ==> 1   //  Any power of 2 will give result as 1
 ```
 
 6. Perform k circular leftshift of n's binary representation. NOTE: n is unsigned int.
```
  Input: n, k
  Output: Resulting integer after k circular shifts
  Sample 1:  1 0        ==>  1
  Sample 2: 21 3        ==>  168
  Sample 3: 3972947 20  ==>  4113564617
 ```
 
  7. Perform k circular rightshift of n's binary representation. NOTE: n is unsigned int.
```
  Input: n, k
  Output: Resulting integer after k right circular shifts
  Sample 1:  1 0        ==>  0
  Sample 2: 21 3        ==>  2684354562
  Sample 3: 3972947 20  ==>  3388289027
```

## Unit 3

### Advanced Programming Constructs
 - [Exercises on Structures, Pointers and Linked List](SPLL.docx)
 
