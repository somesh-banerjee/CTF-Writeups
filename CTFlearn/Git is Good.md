[**problem**](https://ctflearn.com/challenge/104)

You will get a zip file in which there is a ```flag.txt``` file. And the flag in it is incorrect.

From the question we git the hint the flag was earlier there and also it is from github.

Using ```git log``` we can get the info of all the commits and their hash.

Using ```git checkout hash_code``` we can see old commits (replace hash_code with the desired commit hash)

After opening the correct commit we can get the flag simply by ```cat flag.txt```
