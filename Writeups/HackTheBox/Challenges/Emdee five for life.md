# Emdee five for life
Web, 20 Points, Easy

url: http://206.189.17.217:30671/

Now when we visit the page we get a string and a form to submit the md5 hash of the string. The source code of the page is:
```html
<html>
<head>
<title>emdee five for life</title>
</head>
<body style="background-color:powderblue;">
<h1 align='center'>MD5 encrypt this string</h1><h3 align='center'>KHzWjIoONY1yX8yFFQ1I</h3><center><form action="" method="post">
<input type="text" name="hash" placeholder="MD5" align='center'></input>
</br>
<input type="submit" value="Submit"></input>
</form></center>
</body>
</html>
```
Now if we submit the hash manually it will show `Too Slow` irrespective of the fact whether the hash is correct or not.

It is simple we have to submit the hash through script. Before writing the script first we look into the post submission structure. It has only one parameter with key 'hash'.


```python
import requests
import re
import hashlib

url="http://206.189.17.217:30671/"

req = requests.Session()
response = req.get(url)
html = str(response.content)
#x=html[178:198]
clean = re.compile('<.*?>')
x = re.sub(clean, '', str(html))
x = x[54:74]

y = hashlib.md5(x.encode('utf-8')).hexdigest()
data = dict(hash=y)
z = req.post(url, data = data)

print(x)
print(y)
print(z.content)
```
Flag: `HTB{N1c3_ScrIpt1nG_B0i!}`
