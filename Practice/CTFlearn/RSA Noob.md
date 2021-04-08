[**Problem**](https://ctflearn.com/challenge/120)   (Medium,Crypto)

You will get a text file which has the value of e,c,n

```
e: 1
c: 9327565722767258308650643213344542404592011161659991421
n: 245841236512478852752909734912575581815967630033049838269083
```

e is the public key, c is the encrypted message and n is the product of 2 prime nos: p and q

I used an online calculator to find p and q

for decryption we need the private key d, we can get it by using the following formula

```d*e ≡ 1 (mod ϕ(n))```

where ϕ(n) = (p-1)(q-1)    {no. of primes less than n}

by guess we can see here d=1

For decrypting the c to get message m we will use 

```m = c^d (mod n)```

We can see it will be m=c

The decimal is converted into hex and then to ascii to get the text message.
