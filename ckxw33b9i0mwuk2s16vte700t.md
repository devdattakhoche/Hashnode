## What is Binary Exponentiation and How to use it ?

## 📜 Binary Exponentiation


Binary exponentiation is a efficient method of finding  \\( a^b \\), instead of normal multiplicative solution.

You might think, Why do I even use this method when I can find the answer for this using normal multiplication. 

Smart huh!!

![AshoMonaLisaGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641041841485/IpI0eJ_nAi.gif)

### 🔰Problem with trivial Multiplication Method

Consider you have \\( a = 2\\) and \\( b = 3 \\), if you would have to calculate \\( a^b \\) = \\( 2^3 \\), it will be quite simple, right.

$$
2^3 = 2\times 2\times 2  = 8
$$
 
But what if I had given some big numbers such as \\( a = 9999\\) and \\( b = 10248 \\), we see here that number of multiplications required are \\( b = 1024\\), which is quite a lot of work and will take a lot of time.
Furthermore multiplication will take time when we gradually go ahead.

### 📝Solution - Binary Exponentiation

The idea of Binary Exponentiation is that we group the multiplications by dividing its exponent.

In simple words we break \\(b\\) in groups and then carry out the multiplication.


$$
2^{12} = 2\times 2\times 2\times 2\times 2\times 2\times 2\times 2\times 2\times 2\times 2\times 2  
$$

Which can also be written as :

$$
2^{12} = 2^6\times 2^6
$$

Now as you can see, the number of multiplications in the second equation is half that of the first equation. This is called the law of product:

$$
a^b = (a^{(b/2)})^2
$$


![BreakItStitchGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641047067220/45MfSxWcR.gif)

We can further break \\( (b/2) \\) if its possible:

\\[2^8 = 2^4\times 2^4\\]
\\[2^4 = 2^2\times 2^2\\]
\\[2^2 = 2^1\times 2^1\\]

**What if \\( (b) \\) is odd ?**

Well, In that case we can separate the equations as follows :

\\[2^5 = 2^{4+1}\\]
\\[2^5 = 2^4\times 2^1\\]
\\[2^4 = 2^2\times 2^2\\]
\\[2^2 = 2^1\times 2^1\\]

To sum this up : 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641050923514/aeHkGIJ4o.png)

### ⌛Time Complexity Analysis


![TimeClockGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641046948876/dlaxMFodu.gif)

- **Conventional Multiplication method :**

$$
a^b = a\times a..... 
$$

The number of multiplications here are \\( b \\) times, making the time complexity \\( O(b) \\).

- **Binary Exponentiation:**

Now if we see the breakdown of this, it comes out to be like this :



![Blank diagram (1).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641049172652/wYD0vogdL.png)

Calulation :
$$
\frac{b}{2^x} = 1 
$$
$$
b = 2^x
$$
$$
log (b)  = xlog(2)
$$
$$
x = log_2 b
$$

From this we can conclude that we need \\( log(b) \\) operations to complete the tree.
So Time complexity of Binary Exponentiation is \\( O(logb) \\).

### 🧑‍💻 Code


![GimmeCodeCatGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641050986552/eZP8eNwxI.gif)

*Recursive Approach : *
```
int bin_expo(int a, int b){
	if(b==0) return 1;
	int recursive = binExpo(a,b/2);
	if(b & 1) // if b is odd
		return recursive * recursive * a;
	return recursive * recursive;  // if b is even
}

```
As recursive approach uses more memory and are not much better in performance compared to iterative approach, we should use iterative approach :

*Iterative Approach*:
```
int bin_expo(int a, int b){
	int ans = 1;
	while (b>0){
		if (b & 1) // if b is odd 
			ans = (ans *a);
		a = (a *a) ;
		b = b / 2;
	}
	return ans;
}
```

### 🅰️ Applications of Binary Exponentiation

- Finding Modulo Inverse with Fermat's little theorem
- Computation of large exponents 


### 🎯Final thoughts
Binary exponentiation is an important concept when it comes to competitive programming. It is efficient and gives a good performance compared to the conventional method. Generally it comes handy while modular inverse and other similar questions.

<hr/>

Thanks for reading this blog, if you did enjoy reading this please leave a like and comment!✌️
If you like such kind of content, don't forget to follow me on ***Twitter ***and ***Hashnode***!

*Peace out! 😁*

![ImOutGoodbyeGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641056629024/Jrro9wDjP.gif)

