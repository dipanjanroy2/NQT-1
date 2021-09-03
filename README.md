## 1.Command Line Program to Check if a Number is Prime or Not
```
 #include<stdio.h> 
 int main(){
    int n, i, flag = 0;

    printf(“Enter a positive integer: “);
    scanf(“%d”,&n);

    for(i=2; i<=n/2; ++i)
    {
        // condition for nonprime number
        if(n%i==0)
        {
            flag=1;
            break;
        }
    }
    if (flag==0)
        printf(“%d is a prime number.”,n);
    else
        printf(“%d is not a prime number.”,n);
    
    return 0;
}
```

## 2. 1, 2, 1, 3, 2, 5, 3, 7, 5, 11, 8, 13, 13, 17, …….. 
This series is a mixture of 2 series – all the odd terms in this series form a Fibonacci series and all the even terms are the prime numbers in ascending order.
Write a program to find the Nth term in this series.
The value N is a Positive integer that should be read from STDIN.
The Nth term that is calculated by the program should be written to STDOUT.
Other than the value of Nth term, no other characters/strings or message should be written to STDOUT.
For example, when N = 14, the 14th term in the series is 17. So only the value 17 should be printed to STDOUT. 

```
#include<iostream>
#define MAX 99999

using namespace std;

void fibonacci(int n)
{
    /* Variable initialization */
    int a = 0, b = 1, next;
    //the below code is for fibonacci series till nth position
    for (int i = 1; i<=n; i++)
    {
        next = a + b;
        a = b;
        b = next;
    }

    //will print a not b or next as they are stored to calculate next  and next to next term
    cout<< a;
}

void prime(int n)
{
    int i, j, flag, count =0;
    //as prime numbers in given question start from 2
    for (i=2; i<=MAX; i++)
    {
        flag = 0;
        //to check if divisible apart from 1 & itself
        //loop starts from 2 to ignore divisibilty by 1 & ends before the number itself
        for (j=2; j<i; j++)
        {
            if(i%j == 0)
            {
                //number is not prime
                flag = 1;
                break;
            }
        }
        //is prime
        if (flag == 0){
            //if found the nth prime number
            if(++count == n)
            {
                cout<< i;
                break;
            }
        }
    }
}
int main(){
    int n;
    cin >> n;
    
    /*if n is odd
        nth number in main series will be found at (n/2 + 1) position 
        in fibonacci sub series
    else 
        if n is even then it will be found in (n/2) position in prime sub series */
    
    if(n%2 == 1) 
        fibonacci (n/2 + 1);
    else 
        prime(n/2);
    
    
    return 0;
}

```
## Count number of occurrences (or frequency) in a sorted array
Given a sorted array arr[] and a number x, write a function that counts the occurrences of x in arr[]. The expected time complexity is O(Logn)
 Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 2
  Output: 4 // x (or 2) occurs 4 times in arr[]

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 3
  Output: 1 

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 1
  Output: 2 

  Input: arr[] = {1, 1, 2, 2, 2, 2, 3,},   x = 4
  Output: -1 // 4 doesn't occur in arr[]
  
```
// C++ program to count occurrences of an element 
#include<bits/stdc++.h> 
using namespace std; 

// Returns number of times x occurs in arr[0..n-1] 
int countOccurrences(int arr[], int n, int x) 
{ 
    int res = 0; 
    for (int i=0; i<n; i++) 
        if (x == arr[i]) 
        res++; 
    return res; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 2; 
    cout << countOccurrences(arr, n, x); 
    return 0; 
}

```
## Longest Common Subsequence –
Let us discuss Longest Common Subsequence (LCS) problem as one more example problem that can be solved using Dynamic Programming.

LCS Problem Statement: Given two sequences, find the length of longest subsequence present in both of them. A subsequence is a sequence that appears in the same relative order, but not necessarily contiguous. For example, “abc”, “abg”, “bdf”, “aeg”, ‘”acefg”, .. etc are subsequences of “abcdefg”. So a string of length n has 2^n different possible subsequences.

It is a classic computer science problem, the basis of diff(a file comparison program that outputs the differences between two files), and has applications in bioinformatics.

Examples:
LCS for input Sequences “ABCDGH” and “AEDFHR” is “ADH” of length 3.
LCS for input Sequences “AGGTAB” and “GXTXAYB” is “GTAB” of length 4.

```
/* A Naive recursive implementation of LCS problem */
#include<bits/stdc++.h>
int max (int a, int b);

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int
lcs (char *X, char *Y, int m, int n)
{
  if (m == 0 || n == 0)
    return 0;
  if (X[m – 1] == Y[n – 1])
    return 1 + lcs (X, Y, m – 1, n – 1);
  else
    return max (lcs (X, Y, m, n – 1), lcs (X, Y, m – 1, n));
}

/* Utility function to get max of 2 integers */
int
max (int a, int b)
{
  return (a > b) ? a : b;
}

/* Driver program to test above function */
int
main ()
{
  char X[] = “AGGTAB”;
  char Y[] = “GXTXAYB”;

  int m = strlen (X);
  int n = strlen (Y);

  printf (“Length of LCS is %d”, lcs (X, Y, m, n));

  return 0;
}
```
## SubString Problem in C
Given a string as an input. We need to write a program that will print all non-empty substrings of that given string.

```
//substrings of a given string

#include<bits/stdc++.h>
using namespace std;

// Function to print all sub strings
void
subString (char str[], int n)
{
// Pick starting point
  for (int len = 1; len <= n; len++)
    {
// Pick ending point
      for (int i = 0; i <= n – len; i++)
        {
// Print characters from current
// starting point to current ending
// point. 
            int j = i + len – 1;
            for (int k = i; k <= j; k++)
                 cout << str[k];
            cout << endl;
        }
    }
}

// Driver program to test above function
int main ()
{
  char str[] = “abc”;
  subString (str, strlen (str));
  return 0;
}

```
## Pythrogorous Triplets
 
A Pythagorean triplet is a set of three integers a, b and c such that a2 + b2 = c2. Given a limit, generate all Pythagorean Triples with values smaller than given limit.

Input : limit = 20
Output : 3 4 5
         8 6 10
         5 12 13
         15 8 17
         12 16 20
A Simple Solution is to generate these triplets smaller than given limit using three nested loop. For every triplet, check if Pythagorean condition is true, if true, then print the triplet. Time complexity of this solution is O(limit3) where ‘limit’ is given limit.

An Efficient Solution can print all triplets in O(k) time where k is number of triplets printed. The idea is to use square sum relation of Pythagorean triplet, i.e., addition of squares of a and b is equal to square of c, we can write these number in terms of m and n such that,

       a = m2 - n2
       b = 2 * m * n
       c  = m2 + n2
because,
       a2 = m4 + n4 – 2 * m2 * n2
       b2 = 4 * m2 * n2
       c2 = m4 + n4 + 2* m2 * n2
We can see that a2 + b2 = c2, so instead of iterating for a, b and c we can iterate for m and n and can generate these triplets.

Below is the implementation of above idea :
```
// C++ program to generate pythagorean
// triplets smaller than a given limit
#include <bits/stdc++.h>

// Function to generate pythagorean
// triplets smaller than limit
void pythagoreanTriplets (int limit)
{
// triplet: a^2 + b^2 = c^2
  int a, b, c = 0;

// loop from 2 to max_limitit
  int m = 2;

// Limiting c would limit
// all a, b and c
  while (c < limit)
    {

// now loop on j from 1 to i-1
      for (int n = 1; n < m; ++n)
        {

// Evaluate and print triplets using
// the relation between a, b and c
         a = m * m – n * n;
         b = 2 * m * n;
         c = m * m + n * n;
        if (c > limit)
            break;
        printf (“%d %d %d\n“, a, b, c);
        }
      m++;
    }
}

// Driver Code
int main ()
{
  int limit = 20;
  pythagoreanTriplets (limit);
  return 0;
}
```
## Armstrong Number
Given a number x, determine whether the given number is Armstrong number or not. A positive integer of n digits is called an Armstrong number of order n (order is number of digits) if:

abcd... = pow(a,n) + pow(b,n) + pow(c,n) + pow(d,n) + .... 

Input : 153
Output : Yes
153 is an Armstrong number.
1*1*1 + 5*5*5 + 3*3*3 = 153

Input : 120
Output : No
120 is not a Armstrong number.
1*1*1 + 2*2*2 + 0*0*0 = 9

Input : 1253
Output : No
1253 is not a Armstrong Number
1*1*1*1 + 2*2*2*2 + 5*5*5*5 + 3*3*3*3 = 723

Input : 1634
Output : Yes
1*1*1*1 + 6*6*6*6 + 3*3*3*3 + 4*4*4*4 = 1634

```
// C++ program to determine whether the number is
// Armstrong number or not
#include<bits/stdc++.h>
using namespace std;


/* Function to calculate x raised to the power y */
int
power (int x, unsigned int y)
{
  if (y == 0)
    return 1;
  if (y % 2 == 0)
    return power (x, y / 2) * power (x, y / 2);
  return x * power (x, y / 2) * power (x, y / 2);
}

/* Function to calculate order of the number */
int
order (int x)
{
  int n = 0;
  while (x)
    {
      n++;
      x = x / 10;
    }
  return n;
}

// Function to check whether the given number is
// Armstrong number or not
bool
isArmstrong (int x)
{
// Calling order function
  int n = order (x);
  int temp = x, sum = 0;
  while (temp)
    {
      int r = temp % 10;
      sum += power (r, n);
      temp = temp / 10;
    }

// If satisfies Armstrong condition
  return (sum == x);
}

// Driver Program
int
main ()
{
  int x = 153;
  cout << isArmstrong (x) << endl;
  x = 1253;
  cout << isArmstrong (x) << endl;
  return 0;
}
```



