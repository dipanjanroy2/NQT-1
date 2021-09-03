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




