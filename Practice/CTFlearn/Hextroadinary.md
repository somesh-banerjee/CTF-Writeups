[**Problem**](https://ctflearn.com/challenge/158)   (Easy,Crypto)


Read the problem carefully

```
Meet ROXy, a coder obsessed with being exclusively the worlds best hacker. She specializes in short cryptic hard to decipher secret codes.
The below hex values for example, she did something with them to generate a secret code, can you figure out what?
Your answer should start with 0x.

0xc4115 0x4cf8
```

The name ROXy is reverse of XOR. So she did XOR operation on the two codes. You will get the flag just by performing XOR.

```
>>> hex(0xc4115^0x4cf8)
```

Don't forget to add the prefix 0x while submitting
