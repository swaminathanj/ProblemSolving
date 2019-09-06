# Problems on Bitwise operators

## 1. Find the bit at kth position of n's binary representation.
```
  Input: n, k
  Output: 1 if 1 was present at kth position. 0 otherwise.
  Sample 1:  1 0        ==> 1
  Sample 2: 21 4        ==> 1
  Sample 3: 21 3        ==> 0
  Sample 4: 3972947 7   ==> 0
  Sample 5: 3972947 20  ==> 1
 ```
 
## 2. Find if an integer n is negative? i.e. Is leftmost digit set to 1?
```
  Input: n
  Output: YES if n is negative. NO otherwise.
  Sample 1: -1         ==> YES
  Sample 2: 21         ==> NO
  Sample 3: -3972947   ==> YES
  Sample 4: 2147483648  ==> YES //  INT_MAX+1 leads to overflow
  Sample 5: -2147483649  ==> NO  // INT_MIN-1 leads to underflow
```

## 3. Set the bit at kth position of n's binary representation to 1.
```
Input: n, k
  Output: Resulting number after kth bit is made 1
  Sample 1:  1 0        ==> 0
  Sample 2: 21 3        ==> 21
  Sample 3: 3972947 20  ==> 1 
 ```
 
## 4. Set the bit at kth position of n's binary representation to 0.
```
  Input: n, k
  Output: Resulting number after kth bit is made 0
  Sample 1:  1 0        ==> 0
  Sample 2: 21 3        ==> 21
  Sample 3: 3972947 20  ==> 1   
 ```

## 5.  Count the number of 1's in binary representation of n.
 
```
  Input: n
  Output: number of 1's
  Sample 1:  0         ==> 0
  Sample 2: 21         ==> 3
  Sample 3: 2147483647    ==> 31  //  INT_MAX
  Sample 4: 2147483648  ==> 1   //  INT_MAX+1 leads to overflow
  Sample 5: 1024       ==> 1   //  Any power of 2 will give result as 1
 ```
 
## 6. Perform k circular leftshift of n's binary representation. NOTE: n is unsigned int.
```
  Input: n, k
  Output: Resulting integer after k circular shifts
  Sample 1:  1 0        ==>  1
  Sample 2: 21 3        ==>  168
  Sample 3: 3972947 20  ==>  4113564617
 ```
 
##  7. Perform k circular rightshift of n's binary representation. NOTE: n is unsigned int.
```
  Input: n, k
  Output: Resulting integer after k right circular shifts
  Sample 1:  1 0        ==>  0
  Sample 2: 21 3        ==>  2684354562
  Sample 3: 3972947 20  ==>  3388289027
```
