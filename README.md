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
## Counting frequencies of array elements
Given an array which may contain duplicates, print all elements and their frequencies.

Input :  arr[] = {10, 20, 20, 10, 10, 20, 5, 20}
Output : 10 3
         20 4
         5  1

Input : arr[] = {10, 20, 20}
Output : 10 1
         20 2
```
#include <iostream>
using namespace std;
int main()
{
    int freq[100];
    int size, i, j, count;
    /* Input size of array */
    cout << “nEnter size of array: “;
    cin >> size;
    int arr[size];
    /* Input elements in array */
    cout << “nEnter elements in array: “;
    for(i=0; i<size; i++)
    {
        cin >> arr[i];
        /* Initially initialize frequencies to -1 */
        freq[i] = –1;
    }
    for(i=0; i<size; i++)
    {
        count = 1;
        for(j=i+1; j<size; j++)
        {
            /* If duplicate element is found */
            if(arr[i]==arr[j])
            {
                count++;
                /* Make sure not to count frequency of same element again */
                freq[j] = 0;
            }
        }
        /* If frequency of current element is not counted */
        if(freq[i] != 0)
        {
            freq[i] = count;
        }
    }
    /* Print frequency of each element */
    cout << “nFrequency of all elements of array : n”;
    for(i=0; i<size; i++)
    {
        if(freq[i] != 0)
        {
            cout << arr[i] << ” occurs ” << freq[i] << ” times ” << endl;
        }
    }
}

```
## Basic Program for Decimal to Octal
Given a decimal number as input, we need to write a program to convert the given decimal number into equivalent octal number. i.e convert the number with base value 10 to base value 8. The base value of a number system determines the number of digits used to represent a numeric value. For example, the binary number system uses two digits 0 and 1, octal number system uses 8 digits from 0-7 and decimal number system uses 10 digits 0-9 to represent any numeric value.

Examples:

Input : 16
Output : 20

Input : 10
Output : 12

Input: 33
Output: 41

Algorithm:

Store the remainder when the number is divided by 8 in an array.
Divide the number by 8 now
Repeat the above two steps until the number is not equal to 0.
Print the array in reverse order now.
For Example:
If the given decimal number is 16.
Step 1: Remainder when 16 is divided by 8 is 0. Therefore, arr[0] = 0.
Step 2: Divide 16 by 8. New number is 16/8 = 2.
Step 3: Remainder when 2 is divided by 8 is 2. Therefore, arr[1] = 2.
Step 4: Divide 2 by 8. New number is 2/8 = 0.
Step 5: Since number becomes = 0. Stop repeating steps and print the array in reverse order. Therefore the equivalent octal number is 20.
```
// C++ program to convert a decimal
// number to octal number

#include
using namespace std;

// function to convert decimal to octal
void decToOctal (int n)
{

// array to store octal number
  int octalNum[100];

// counter for octal number array
  int i = 0;
  while (n != 0)
    {

// storing remainder in octal array
      octalNum[i] = n % 8;
      n = n / 8;
      i++;
    }

// printing octal number array in reverse order
  for (int j = i – 1; j >= 0; j–)
    cout << octalNum[j];
}

// Driver program to test above function
int main ()
{
  int n = 33;

  decToOctal (n);

  return 0;
}
```
## Basic Program for Binary to Octal Conversion
Given a binary number as input, we need to write a program to convert the given binary number into equivalent octal number. i.e convert the number with base value 2 to base value 8. The base value of a number system determines the number of digits used to represent a numeric value. For example, the binary number system uses two digits 0 and 1, octal number system uses 8 digits from 0-7 and decimal number system uses 10 digits 0-9 to represent any numeric value.

```
#include<stdio.h>
void main(int argc,char *argv[])
{ 
   long int n,r,c,b=1,s=0;
    n=atoi(argv[1]);
    c=n;
    while(c!=0)
    {
    r=c%10;
    s=s+r*b;
    c=c/10;
    b=b*2;
  }
    printf(“%lo”,s);
    getch();
}
```
## Program To check if a year is Leap year or not
```
#include<stdio.h>


int main ()
{
  int year;
  printf (“Enter a year: “);
 scanf (“%d”, &year);

  if (year % 4 == 0)

    {

      if (year % 100 == 0)

    {

// year is divisible by 400, hence the year is a leap year

      if (year % 400 == 0)

        printf (“%d is a leap year.”, year);

      else

        printf (“%d is not a leap year.”, year);

    }

      else

    printf (“%d is a leap year.”, year);

    }

  else

    printf (“%d is not a leap year.”, year);


  return 0;

}
```
```
#include <stdio.h>
void main (int argc, char *argv[])
{
  int n;
  n = atoi (argv[1]);
  if (n % 4 == 0)
    {
      if (n % 100 == 0)
    {
      if (n % 400 == 0)
        printf (“Leap Year”);
      else
        printf (“Not Leap Year”);
    }
      else
    printf (“Leap Year”);
    }
  else
    printf (“Not Leap Year”);
  getch ();
}
```

## Command Line Program to Check if a Number is Prime or Not
```
#include<stdio.h>

int main (int argc, char *argv[])
{
  int n, i, flag = 0;
  n = atol (argv[1]);
  for (i = 2; i <= n / 2; ++i)
    {
      if (n % i == 0)
      {
      flag = 1;
      break;
      }
    }
  if (flag == 0)
    printf (“%d is a prime number.”, n);
  else
    printf (“%d is not a prime number.”, n);
  return 0;
}
```
```
#include<stdio.h> 
int main()
{
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
## Command Line Program to Reverse a Number
```
#include<stdio.h>
#include<conio.h>
int main (int argc, char *argv[])
{
  if (argc == 1)
    {
      printf (“No Arguments”);
      return 0;
    }
  else
    {
      int n, reverseNumber, temp, rem;
      n = atoi (argv[1]);
      temp = n;
      reverseNumber = 0;
      while (temp)
    {
      rem = temp % 10;
      reverseNumber = reverseNumber * 10 + rem;
      temp = temp / 10;
    }
      printf (“%d”, reverseNumber);
      return 0;
    }
}
```
```

#include <stdio.h>
int main()
{
    int n, reversedNumber = 0, remainder;

    printf(“Enter an integer: “);
    scanf(“%d”, &n);

    while(n != 0)
    {
        remainder = n%10;
        reversedNumber = reversedNumber*10 + remainder;
        n /= 10;
    }

    printf(“Reversed Number = %d”, reversedNumber);

    return 0;
}
```
## Reverse a string without inbuilt Functions
```
#include <iostream>
using namespace std;

int main()
{
   char s[1000], r[1000];
   int begin, end, count = 0;

   cout << “Input a string\n“;
   cin >> s;

   // Calculating string length

   while (s[count] != ‘\0‘)
      count++;

   end = count – 1;

   for (begin = 0; begin < count; begin++) {
      r[begin] = s[end];
      end–;
   }

   r[begin] = ‘\0‘;

   cout << r;

   return 0;
}
```
##  Write a program to convert a number to its binary equivalent and print the bit representation of the number.
```
#include<stdio.h>
void binary (unsigned int);
void main ()
{
  unsigned int num;
  printf (“Enter Decimal Number : “);
  scanf (“%u”, &num);
  binary (num);
}

void binary (unsigned int num)
{
  unsigned int mask = 0x80000000;
  printf (“\nThe Binary Number is : “);
  while (mask > 0)
    {
      if ((num & mask) == 0)
    printf (“0”);
      else
    printf (“1”);
      mask = mask >> 1;
    }
  printf (“\n“);
}

22
```
## Write a program that will take a number in integer format and convert it and print it in string format. For e.g.,

Input Integer => 574
Output String => “574”

```
#include<stdio.h>
#include<stdlib.h>
int main ()
{
  int number, nitems;
  char clear[25];
  char token[25];
  printf (“\nPlease enter a number: “);
  fflush (stdin);
  nitems = scanf (“%d”, &number);
  while (nitems != 1)
    {
    /* Clear the Buffer */
      gets (clear);
      printf (“\nPlease enter a number digits only: “);
      nitems = scanf (“%d”, &number);
    }
  printf (“\nThe number of items scanned = %d”, nitems);
  sprintf (token, “%d “, number);
  printf (“\nThe number % d is converted into string:%s \n“, number, token);
}

```
### 20 Read from a File
Write a program to print the number of characters and lines in a file. You should ignore the space, tab and newline characters for the character count

Create a file called input.txt in the same directory as this file and enter some lines of text or copy a paragraph of text. The filename should be input.txt
```

#include <stdio.h>
#include <string.h>
int main ()
{
  FILE *fp;
  int line_count = 0, char_count = 0;
  char c;
  fp = fopen (“input.txt”, “r”);
  if (fp == NULL)
    {
      printf (“\nThe file cannot be opened in read mode\n“);
      exit (1);
    }
  c = fgetc (fp);
  while (c != EOF)
    {
/* If the character read is a newline or tab or space */
      if (c == ‘\n‘ || c == ‘\t‘ || c == ‘\b‘)
    {
/* If it is a newline character increment the line count */
      if (c == ‘\n‘)
        line_count++;
/* Read the next character from the file */
      c = fgetc (fp);
/* Continue with the next iteration */
      continue;
    }
/* Since the character is not a newline, tab or space increment
the character count
*/
      char_count++;
      c = fgetc (fp);
    }
/* Since we are done processing the entire file we print the
the charcter count and the word count for the file
*/
  printf (“\n The number of characters = %d\n“, char_count);
  printf (“\n The number of lines = %d\n“, line_count);
  return 0;
}

```
## Write a program that will take a number in string format and convert it and print it in an integer format. For e.g.,

Input String => ”574”
Output Integer => 574

```
#include<stdio.h> 
#include<math.h>

int main() 
{ 
    char str[1000], i=0,num=0; 
    scanf(“%s”,str);
    // in Ascii 48 – 57 represent 0 – 9
    // subtracting 48 from each will give us actual value in int
    while(str[i]!=‘\0‘){
        num = str[i] – 48;
        printf(“%d”,num);
        i++;
    }
    return 0; 
}

```
## Addition of 2 numbers and printing the result in binary Using Command Line Programming
```
#include <stdio.h>

int main (int argc, char *argv[])
{
  int sum;
  if (argc == 1)
    {
      printf (“enter number : “);
    }
  else
    {
      int i, j, r, a[10];
      sum = atoi (argv[1]) + atoi (argv[2]);
      printf (“sum %d\n“, sum);
      for (i = 0; sum > 0; i++)
        {
            r = sum % 2;
            a[i] = r;
            sum = sum / 2;
        }
      printf (“binary format is\n“);
      for (j = i – 1; j >= 0; j++)
        {
            printf (“%d”, a[j]);
        }
    }
  return 0;
}
```
## Sum of prime numbers in a given range 
Given a range [l, r], the task is to find the sum of all the prime numbers within that range.

Examples:

Input : l=1 and r=6
Output : 10
2 + 3 + 5

Input : l=4 and r=13
Output : 36
5 + 7 + 11 + 13 = 36
```
#include <iostream> 
using namespace std; 

// Method to compute the prime number 
// Time Complexity is O(sqrt(N)) 
bool checkPrime(int numberToCheck) 
{ 
    if(numberToCheck == 1) { 
        return false; 
    } 
    for (int i = 2; i*i <= numberToCheck; i++) { 
        if (numberToCheck % i == 0) { 
            return false; 
        } 
    } 
    return true; 
} 

// Method to iterate the loop from l to r 
// If the current number is prime, sum the value 
int primeSum(int l, int r) 
{ 
    int sum = 0; 
    for (int i = r; i >= l; i–) { 
        // Check for prime 
        bool isPrime = checkPrime(i); 
        if (isPrime) { 
            // Sum the prime number 
            sum = sum + i; 
        } 
    } 
    return sum; 
} 
// Time Complexity is O(r x sqrt(N)) 

//Driver code 
int main() 
{ 
    int l = 4, r = 13; 
    // Call the method with l and r 
    cout << primeSum(l, r); 
} 
```
## Second Largest Number in an Array
Given an array of integers, our task is to write a program that efficiently finds the second largest element present in the array.

Example:

Input : arr[] = {12, 35, 1, 10, 34, 1}
Output : The second largest element is 34.

Input : arr[] = {10, 5, 10}
Output : The second largest element is 5.

Input : arr[] = {10, 10, 10}
Output : The second largest does not exist.

```
// C program to find second largest  
// element in an array 

#include <stdio.h> 
#include <limits.h>  

/* Function to print the second largest elements */
void print2largest(int arr[], int arr_size) 
{ 
    int i, first, second; 

    /* There should be atleast two elements */
    if (arr_size < 2) 
    { 
        printf(” Invalid Input “); 
        return; 
    } 

    first = second = INT_MIN; 
    for (i = 0; i < arr_size ; i ++) 
    { 
        /* If current element is greater than first 
           then update both first and second */
        if (arr[i] > first) 
        { 
            second = first; 
            first = arr[i]; 
        } 

        /* If arr[i] is in between first and  
           second then update second  */
        else if (arr[i] > second && arr[i] != first) 
            second = arr[i]; 
    } 
    if (second == INT_MIN) 
        printf(“There is no second largest element\n“); 
    else
        printf(“The second largest element is %dn”, second); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {12, 35, 1, 10, 34, 1}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    print2largest(arr, n); 
    return 0; 
} 
```
## GCD of  Three Numbers
 
 
Definition of HCF (Highest common factor):

HFC is also called the greatest common divisor (gcd). HCF of two numbers is the largest positive number which can divide both numbers without any remainder. For example, the HCF of two numbers 4 and 8 is 2 since 2 is the largest positive number which can divide 4 as well as 8 without a remainder.

The logic for writing program:

It is clear that any number is not divisible by greater than the number itself.

☆In the case of more than one number, a possible maximum number that can divide all of the numbers must be a minimum of all of that numbers.

For example 10, 20, and 30
Min (10, 20, 30) =10 can divide all there numbers. So we will take one for loop which will start from the min of the numbers and will stop the loop when it became one since all numbers are divisible by one. Inside for loop, we will write one if conditions which will check divisibility of both the numbers.
```
#include<stdio.h>
int gcd (int, int, int);
int main ()
{
  int i, j, k, g;
  scanf (“%d %d %d”, &i, &j, &k);

  g = gcd (i, j, k);
  printf (“%d”, g);

  return 0;
}

int gcd (int i, int j, int k)
{
  int least;
  least = i;
  while (!((i == j) && (j == k)))
    {
      i = (i == 0 ? least : i);
      j = (j == 0 ? least : j);
      k = (k == 0 ? least : k);
      if (i <= j)
    {
      if (i <= k)
        least = i;
      else
        least = k;
    }
      else
    {
      if (j <= k)
        least = j;
      else
        least = k;
    }
      i = i % least;
      j = j % least;
      k = k % least;
    }
  return least;
}
```



