Maximum profit by buying and selling a share atmost twice in C++
 

Here, in this page we will discuss the program to find maximum profit by buying and selling a share atmost twice in C++ .
In daily share trading, a buyer buys shares in the morning and sells them on the same day. If the trader is allowed to make at most 2 transactions in a day, whereas the second transaction can only start after the first one is complete Buy->Sell->Buy->Sell. We are given with stock prices throughout the day, We need to  find out the maximum profit that a share trader could have made.

Maximum profit by buying and selling a share atmost twice in C++
Method 1 :
Create an array say profit of size n and initialize all its value to 0.
Iterate price[] from right(n-1) to left(0) and update profit[i] such that profit[i] stores maximum profit achievable from one transaction in sub-array price[i..n-1].
Iterate price[] from left to right and update profit[i] such that profit[i] stores maximum profit such that profit[i] contains maximum achievable profit from two transactions in sub-array price[0..i].
After completing the iteration print value of profit[n-1].
Time-Space Complexities :
Time – complexity : O(n)
Space – complexity : O(n)
Maximum profit in C++
Code to find Maximum profit by buying and selling a share atmost twice in C++
#include <bits/stdc++.h>
using namespace std;

int maxProfit(int price[], int n)
{
   // Create profit array and
   // initialize it as 0
   int profit[n];
   for (int i = 0; i < n; i++)
       profit[i] = 0;

   int max_price = price[n - 1];
   for (int i = n - 2; i >= 0; i--) {
     if (price[i] > max_price)
      max_price = price[i];
     profit[i] = max(profit[i + 1], max_price - price[i]);
   }

   int min_price = price[0];
   for (int i = 1; i < n; i++) {
       // min_price is minimum price in price[0..i]
       if (price[i] < min_price)
          profit[i] = max(profit[i - 1],profit[i] + (price[i] - min_price));
   }
  int result = profit[n - 1];
  delete[] profit; // To avoid memory leak
  return result;
}

// Driver code
int main()
{ 
  int n;
  cin>>n;

  int price[n];
  for(int i=0; i<n; i++) cin>>price[i];
  cout << "Maximum Profit = " << maxProfit(price, n);
  return 0;
}
Input : 

7

2, 30, 15, 10, 8, 25, 80 

Output :

maximum Profit = 100

Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Minimum no. of Jumps to reach the end of an array 

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 :
Initialize four variables for taking care of the first buy, first sell, second buy, second sell.
Set first buy and second buy as INT_MIN and first and second sell as 0.
This is to ensure to get profit from transactions.
Iterate through the array and return the second buy as it will store maximum profit.
Time-Space Complexities :
Time – complexity : O(n)
Space – complexity : O(1)
Code to find Maximum profit by buying and selling a share atmost twice in C++
#include <bits/stdc++.h>
using namespace std;

int maxProfit(int arr[], int n)
{
      int first_buy = INT_MIN;
     int first_sell = 0;
     int second_buy = INT_MIN;
     int second_sell = 0;      
     for(int i=0;i<n;i++) {    
          first_buy = max(first_buy,-arr[i]);
          first_sell = max(first_sell,first_buy+arr[i]);
          second_buy = max(second_buy,first_sell-arr[i]);
          second_sell = max(second_sell,second_buy+arr[i]);
    }
     return second_sell;
}

// Driver code
int main()
{ 
int n;
cin>>n;

int price[n];
for(int i=0; i<n; i++) cin>>price[i];
cout << "Maximum Profit = " << maxProfit(price, n);
return 0;
}
Input : 

7

2, 30, 15, 10, 8, 25, 80 

Output :

maximum Profit = 100
