[**Problem**](https://ctflearn.com/challenge/174)

We have to create a program which will read the number of lines with the given properties

My code is

```
file = open("data.txt","r")
even=0
count=0
odd=0
for line in file:
	even=0
	odd=0
	for ch in line:
		if (ch == '1'):
			even=even+1
		elif (ch == '0'):
			odd=odd+1
	if (e%2==0 or o%3==0):
		count=count+1

print(c)
```
You try to make the code by yourself.
