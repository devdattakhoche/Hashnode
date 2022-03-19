## Binary Search : Explain Like I am five

## Hey Everyone 👋👋 

I hope you all are doing fine! 🌟

Searching is a big part of everything, we can see multiple use cases of searching, such as searching books, Posts, etc.

Did you know?

>  The number of searches performed on search engines each year is at least 2 Trillion 🤯🤯


So by now, you might have got a fair idea of how important searching is. Now let us get to the famous egg problem, which will help us understand binary search in a really simple way.



![SherlockProblemGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647660319284/kjGaYSeM_.gif)


## 🥚Egg Problem

Consider that you are on a 100 story building and you have a lot of eggs. You want to find the highest floor such that if you throw an egg from that floor, the egg wouldn't crack. You really want to do it as fast as possible. What would your approach be? 🤔🤔

If you throw an egg from a certain floor and it breaks then it will also break if you throw it from a relatively higher floor.
 
PS:  Don't try this in the real world, the egg will definitely break 😂😂

Take some time to understand the problem.


#### 🎯 Basic Approach 


![JustBasicStuffNormalGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647660637880/VftUbSAjH.gif)

This approach is really simple, probably you might have this solution already in your mind.
Also, keep in mind that if you throw an egg from a certain floor and it breaks then it will also break if you throw it from a relatively higher floor.
 

So basically we are searching for the highest floor from which if we throw an egg it won't break. Here is the basic approach for searching this floor :


1. Go to the first floor and throw the egg.
2. If it breaks then there is no floor such that the egg won't break. 
3. If it does not break, we go to the second floor and throw the egg 
4. If it breaks then you have found the highest 
floor such that the egg won't break, that is the first floor.
5. If it does not break, we go to the third floor and throw the egg 
6. If it breaks then you have found the highest 
floor such that the egg won't break, that is the second floor.
7. If it does not break, we go to the next floor and throw the egg.
8. We do this until we find the answer that is the highest floor.


Now if the answer would have been the 37th floor, this approach will take 38 tries of throwing the egg as you will also try the 38th floor just to find out that the egg will break if thrown from here or from higher floors. 🥚

Can we do this a bit faster? 🤔🤔

#### 🎯 Binary Search approach

Here is where binary search comes into play. I can guarantee you, that you will feel better after reading this approach.😅😅

Consider the answer as 37 in this case and we find 37 by this approach.

1. The idea is to start from the middle of the 
highest (100th) and lowest (1st) floor which is
we first check on the 50th floor.
2. If it breaks that means it will also break for all the above floors.
So we only have 49 more floors left to search from,
as we know the result for the 50th floor. 
3. If it doesn't break we only need to search for 
floors  51 (lowest) to 100 (highest).
As the answer is 37th floor we know it will break.
3. Again we do the same thing as we have done in the 
first step but this time our highest floor will become 49th floor 
as we know that if we throw an egg from floors above 49, it will break
4. So we again choose the middle of the highest floor (49th) and 
the lowest floor(1st) which is the 25th floor.
5. On the 25th floor it won't break as the answer is 37, so we know that our answer lies in between 26 and 49, so we again choose the middle of lowest (26) and highest (49)
6. Now we again take the middle floor of the lowest (26) and highest (49), which is 37.
7. We drop the egg from the 37th floor, as the answer is 37th floor, the egg won't break.
8. Now we need to search only from the 38th floor to the 49th floor.
9. We use the same approach and in each try, the egg will break as the answer is 37th floor.
10. You do this until you have the information on all the floors.

When you complete all the trials here is how you have moved : 

```
Lowest floor : 1| Highest floor : 100| Middle Floor : 50
Will the Egg break if thrown from 50 floor ? Yes
Lowest floor : 1| Highest floor : 49| Middle Floor : 25
Will the Egg break if thrown from 25 floor ? No
Lowest floor : 26| Highest floor : 49| Middle Floor : 37
Will the Egg break if thrown from 37 floor ? No
Lowest floor : 38| Highest floor : 49| Middle Floor : 43
Will the Egg break if thrown from 43 floor ? Yes
Lowest floor : 38| Highest floor : 42| Middle Floor : 40
Will the Egg break if thrown from 40 floor ? Yes
Lowest floor : 38| Highest floor : 39| Middle Floor : 38
Will the Egg break if thrown from 38 floor ? Yes
Amazing the answer is : 37
```

## 🧑‍💻Code


![GimmeCodeCatGIF (2).gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647660811138/TkxyfRvzC.gif)


Here is an iterative code for the Egg break problem, considering the answer to be 37th floor.

```
#include<bits/stdc++.h>
using namespace std;

bool eggBreak(int ans){
    if(ans > 37)
        return true;
    else
        return false;
}

int binarySearch(int l,int h){

    int ans = -1;
    while( l < h ){
        int mid = l + (h - l) / 2;
        
        if(eggBreak(mid)){
            h = mid - 1;
        }
        else{
            ans = mid;
            l = mid + 1;
        }
    }
    return ans;
}

int main(){
    cout<<binarySearch(1,100)<<endl;
}

```
Now that you have got a fair idea of what is binary search, let us understand `upper bound` and `lower bound`.

#### 📜LowerBound

Consider that you have sorted array and number `x`, you want to find the lower bound of `x`. Lowerbound of `x` means the next smallest number just greater than or equal to that of `x`.

```
Eg :
Array : 1 2 3 4 5 7
lower bound of 2 is 2.
lower bound of 6 is 7.
```
We use the same binary search approach here to find the lower bound.

Here `a` is the sorted array, `n` is the length of the array, `x` is the element for which we want to find the lowerbound

```
int lowerbound(int a[], int n, int x) {
    int l = 0;
    int h = n;
    while (l < h) {
        int mid =  l + (h - l) / 2;
        if (x <= a[mid]) {
            h = mid;
        } else {
            l = mid + 1;
        }
    }
    return l;
}
```
#### 📜UpperBound

Upperbound of element `x` means the first element that is strictly greater than the specified value `x`.

```
Eg :
Array : 1 2 3 4 5 7
upperbound of 2 is 3.
upperbound of 6 is 7.
```
We use the same binary seacrh approch as we used in lowerbound.
Here `a` is the sorted array, `n` is the length of the array, `x` is the element for which we want to find the upper bound.


```
int upper_bound(int a[], int n, int x) {
    int l = 0;
    int h = n;
    while (l < h) {
        int mid =  l + (h - l) / 2;
        if (x >= a[mid]) {
            l = mid + 1;
        } else {
            h = mid;
        }
    }
    return l;
}
```


***Note : We can see in the above problems the sequence on which were using binary search, is always sorted. So remember binary search can only be applied when the sequence is sorted.***


## ⌛ Time Complexity Analysis


![JoniCvetkovskiTimeIsMoneyGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647663610694/aW1l-1f0u.gif)

The time taken by binary search on a sequence of length `n` is of the order of `log(n)`
In Every iteration, we shrink the length of the array by 2. We do this until the length of the search range is reduced to 1.


Calculation : 

$$ \frac{n}{2^x} = 1 $$ $$ n = 2^x $$ 
$$ log (n) = xlog(2) $$ 
$$ x = log_2 n $$
$$ x = O(log n) $$

## 🎯Final Thoughts

Congrats on making it to the end of the article! 🌟🌟

Binary Search is a really good concept in itself, it makes the searching process blazingly fast. Personally, I really love problems related to binary search.😅

The most important part is to understand when to use and when not to use the binary search, this will help you break down a lot of doubts while solving problems.

To get a hang of this concept, you can try this [problem](https://leetcode.com/problems/peak-index-in-a-mountain-array/solution/).


***I hope you have enjoyed this article!  Bye-bye! 👋🙋‍♂️***

![SizzleSizzlebrothersGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647691429705/8eA5BfHcg.gif)
