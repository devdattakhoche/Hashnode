## Modulo in Competitive Programming - 1e9 + 7

## Hey Everyone 👋👋

In this article, we will understand some really basic modulo operations and applications for the same.

Now, Modulo in mathematics is a simple operation that returns the remainder when one integer is divided by another, simple isn't it, Smarty-pants!

![MeetTheRobinsonsSmartypantsGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1642695551221/ivX5VqDbw.gif)

Essentially we can sum it up like this probably :

```
Dividend = Divisor × Quotient + Remainder 
Example : 
--> 15 = 2 x 7 + 1 
--> 15 mod 2 = 1
Here 1 is the remainder of 15 when divided by 2
```
Also, the modulo operator in most of the programming languages is denoted by `%`.
```
15 % 2 = 1
```

### ➕Addition 
 
Addition with modulo is quite simple : 

```
// Addition

(a + b) % mod = ((a % mod) + (b % mod)) % mod

Eg : 

(15 + 3) % 10 = 18 % 10 = 8

Expanding the brackets :

(15 + 3) % 10 
= ((15 % 10) + (3 %10)) % 10 
= (5 + 3) % 10 
= 8 % 10 = 8

```

### ❌ Multiplication 

Multiplication with modulo is the same as addition

```
// Multiplication

(a x b) % mod = ((a % mod ) x (b % mod)) % mod

Eg : 

(4 x 12) % 10 
= (48) % 10 
= 8

Expanding the brackets 

(4 x 12) % 10 
= ((4 % 10) x (12 % 10)) % 10
= (4 x 2) % 10
= 8 % 10
= 8


```

### ➖ Subtraction 

Subtraction with modulo is a bit tricky
You can't do subtraction with the mod operator as you do it with addition and multiplication. Subtraction is a bit strange.

```
// Subtraction

(a - b) % mod = ((a  % mod )  - (b % mod) + mod) % mod

Eg :

(11 - 3) % 10  = 8

Expanding the brackets : 

= ((11 % 10) - (3 % 10) + 10) % 10 
= (1 -3 + 10 ) %10
=  8 % 10 = 8
```

Now if try to program it,
we don't have to add mod every single time. We can do this :

```
// We can do this 
int ans = ((x - y) % mod);
if(ans< 0) // if x < y then add mod 
  ans+=mod

// or 

int ans = ((x - y) % mod + mod)%mod;  // Slower than above

```

### ➗Division

The division under mod operator is not the same as addition and is very different.

```
(a / b) % mod may NOT be same as ((a % mod)/(b % mod)) % mod

```
Now, Modular division does not always exist. We can only do modular division if the is modular inverse of the divisor exists. 

> Modular Multiplicative inverse of two numbers exists only and only if `gcd` of those two numbers is equal to 1 that they are relatively prime.

> Two integers are relatively prime when there are no common factors other than 1.

So to sum this up :

```
a / b  = a x 1/b 

(a / b) % mod = (a x (inverse of b if exists)) % mod

```
Here is the program for the same :

```

#include<bits/stdc++.h>
using namespace std; 

#define mod 23

int bin_expo(int a, int b){
    int ans = 1;
    while (b>0){
        if (b & 1) // if b is odd 
            ans = (ans *a) % mod;
        a = (a *a) % mod ;
        b = b / 2;
    }
    return ans;
}

int modInverse(int a){ // inverse by fermats theorem
    int g = __gcd(a, mod);
    if (g != 1)
        return -1;
    else{
        // If a and m are relatively prime, then modulo
        // inverse is a^(m-2) mode m
        return bin_expo(a,mod-2);
    }
}

int modDivide(int a, int b){
    a = a % mod;
    int inv = modInverse(b); 
    if (inv == -1)
       return (-1);
    return (inv * a) % mod;
}

signed main(){
    int  a  = 8, b = 3;
    int ans = modDivide(a, b);
    return cout<<ans<<endl,0;    
}
```


## 🎯 Final Thoughts

Modulus is crucial and a necessary operator in competitive programming.
If you know this it can help you with multiple questions.


[Here](https://www.codechef.com/problems/CNTARRAY) is a good question if you want to get a hang of it.

Also, do watch this [explaination](https://www.youtube.com/watch?v=-OPohCQqi_E) from Errichto, this is where I learned it from.


Congrats🎉🎉 on making it to the end of the article! Have a good day!
Stay tuned for such content! 👋✌️


![ThumbsUpNiceGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1642874353966/zQMR23JHF.gif)


