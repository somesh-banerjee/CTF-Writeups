CTF page : https://ctf.hsctf.com/

## misc/sanity-check
> **HSN CS Club**\
> Have a free flag!

flag - ` flag{1m_g0in6_1ns@ne_1m_g0in6_1ns@ne_1m_g0in6_1ns@ne} `
***
## web/NRC
> **goose**\
Find the flag :)\
[no-right-click.hsc.tf](https://no-right-click.hsc.tf/)

Right click was disaled in the page. So we have to use keyboard shortcuts to open developers tools. There is a css file in which got the flag.

flag - `flag{keyboard_shortcuts_or_taskbar}`
***
## misc/discord-flag
> **HSN CS Club**\
Join the discord server! The flag will be in the channel description of #general.

flag - `flag{we1c0me_t0_hsctf!}`
***
## misc/Return of the Intro to Netcat
> **meow**\
hey, netcat seems fun! (with a twist)
`nc return-of-the-intro-to-netcat.hsc.tf 1337`

Run the above code and you will get this output
```
== proof-of-work: enabled ==
please solve a pow first
You can run the solver with:
    python3 <(curl -sSL https://goo.gle/kctf-pow) solve s.AACF.AABf32fAGFfRbIo+4bAc4Ldz
===================

Solution?
```
Visit the link to learn about the source code. The source code can ask the difficulty of a challenge or solve it. Now run the python3 code in terminal to get the solution and pass it to above command to get flag.

flag - `flag{the_cat_says_meow}`
***
## crypto/queen-of-the-hill
> **wooshi**\
After finding a special key of the Hill, which contains a note to visit the Queen of the Hill, our brave Amanda begins her adventure to find the Queen of the Hill’s treasure. How shall she meet the Queen of the Hill? (a=0)\
Cipher text: rtca{vbuhp_kaiq_gfj_nx_rda_ujw}\
Encryption key:\
16 25 8\
14 19 5\
15 17 3

From the Encryption key I understood it is a hill Cipher which uses a square matrix as key. By using [Dcode.fr](https://www.dcode.fr/hill-cipher) I got the flag.

flag - `flag{climb_your_way_to_the_top}`
***
## crypto/aptenodytes-forsteri
> **AC**\
Here's a warmup cryptography challenge. Reverse the script, decrypt the output, submit the flag.\
Attachments:\
*output.txt*
```
IOWJLQMAGH
```
*aptenodytes-forsteri.py*
```
flag = open('flag.txt','r').read() #open the flag
assert flag[0:5]=="flag{" and flag[-1]=="}" #flag follows standard flag format
letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
encoded = ""
for character in flag[5:-1]:
    encoded+=letters[(letters.index(character)+18)%26] #encode each character
print(encoded)
```

This is simple shift cipher and it can be reversed by just performing subtraction instead of addition on the encoded string. Here is the code:
```
encoded = 'IOWJLQMAGH'
decoded = ''
letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
for character in encoded:
	decoded += letters[(letters.index(character)-18)%26]
print('flag{'+decoded+'}')
```

flag - `flag{QWERTYUIOP}`
***
## crypto/opisthocomus-hoazin
> **AC**\
> The plural of calculus is calculi.\
> Attachments:\
*output.txt*
```
15888457769674642859708800597310299725338251830976423740469342107745469667544014118426981955901595652146093596535042454720088489883832573612094938281276141337632202496209218136026441342435018861975571842724577501821204305185018320446993699281538507826943542962060000957702417455609633977888711896513101590291125131953317446916178315755142103529251195112400643488422928729091341969985567240235775120515891920824933965514217511971572242643456664322913133669621953247121022723513660621629349743664178128863766441389213302642916070154272811871674136669061719947615578346412919910075334517952880722801011983182804339339643
65537
[65639, 65645, 65632, 65638, 65658, 65653, 65609, 65584, 65650, 65630, 65640, 65634, 65586, 65630, 65634, 65651, 65586, 65589, 65644, 65630, 65640, 65588, 65630, 65618, 65646, 65630, 65607, 65651, 65646, 65627, 65586, 65647, 65630, 65640, 65571, 65612, 65630, 65649, 65651, 65586, 65653, 65621, 65656, 65630, 65618, 65652, 65651, 65636, 65630, 65640, 65621, 65574, 65650, 65630, 65589, 65634, 65653, 65652, 65632, 65584, 65645, 65656, 65630, 65635, 65586, 65647, 65605, 65640, 65647, 65606, 65630, 65644, 65624, 65630, 65588, 65649, 65585, 65614, 65647, 65660]
```
*opisthocomus-hoazin*
```
import time
from Crypto.Util.number import *
flag = open('flag.txt','r').read()
p = getPrime(1024)
q = getPrime(1024)
e = 2**16+1
n=p*q
ct=[]
for ch in flag:
    ct.append((ord(ch)^e)%n)
print(n)
print(e)
print(ct)
```

This is a RSA Encryption challenge. The n is too large for RSActftool or factordb. So I have to brute force the value of d with the following code.
```
n = 15888457769674642859708800597310299725338251830976423740469342107745469667544014118426981955901595652146093596535042454720088489883832573612094938281276141337632202496209218136026441342435018861975571842724577501821204305185018320446993699281538507826943542962060000957702417455609633977888711896513101590291125131953317446916178315755142103529251195112400643488422928729091341969985567240235775120515891920824933965514217511971572242643456664322913133669621953247121022723513660621629349743664178128863766441389213302642916070154272811871674136669061719947615578346412919910075334517952880722801011983182804339339643
e = 65537
ct = [65639, 65645, 65632, 65638, 65658, 65653, 65609, 65584, 65650, 65630, 65640, 65634, 65586, 65630, 65634, 65651, 65586, 65589, 65644, 65630, 65640, 65588, 65630, 65618, 65646, 65630, 65607, 65651, 65646, 65627, 65586, 65647, 65630, 65640, 65571, 65612, 65630, 65649, 65651, 65586, 65653, 65621, 65656, 65630, 65618, 65652, 65651, 65636, 65630, 65640, 65621, 65574, 65650, 65630, 65589, 65634, 65653, 65652, 65632, 65584, 65645, 65656, 65630, 65635, 65586, 65647, 65605, 65640, 65647, 65606, 65630, 65644, 65624, 65630, 65588, 65649, 65585, 65614, 65647, 65660]

d=0
while(1):
	if(ord('f') == (ct[0]^d)%n):
		break
	d=d+1

dec=''
for i in ct:
	dec += chr((i^d)%n)
```
d value 65537

flag - `flag{tH1s_ic3_cr34m_i5_So_FroZ3n_i"M_pr3tTy_Sure_iT's_4ctua1ly_b3nDinG_mY_5p0On}`
***
## misc/pallets-of-gold
> **cppio**\
> It doesn't really look like gold to me...\
> Attachments: pallets-of-gold.png\

The picture was noisy. Using [this tool](online.georgeom.net) and changing the bits plane got the flag.
flag - `flag{}`
***
## web/message-board
> **goose**\
> Your employer, LameCompany, has lots of gossip on its company message board: message-board.hsc.tf. You, Kupatergent, are able to access some of the tea, but not all of it! Unsatisfied, you figure that the admin user must have access to ALL of the tea. Your goal is to find the tea you've been missing out on.\
Your login credentials: username: kupatergent password: gandal\
Server code is attached\
> Attachments:\
> *app.js:*
> ```
> const express = require("express")
> const cookieParser = require("cookie-parser")
> const ejs = require("ejs")
> require("dotenv").config()
>
> const app = express()
app.use(express.urlencoded({ extended: true }))
app.use(cookieParser())
app.set("view engine", "ejs")
> app.use(express.static("public"))
>
> const users = [
    {
        userID: "972",
        username: "kupatergent",
        password: "gandal"
    },
    {
        userID: "***",
        username: "admin"
    }
]
>
> app.get("/", (req, res) => {
    const admin = users.find(u => u.username === "admin")
    if(req.cookies && req.cookies.userData && req.cookies.userData.userID) {
        const {userID, username} = req.cookies.userData
        if(req.cookies.userData.userID === admin.userID) res.render("home.ejs", {username: username, flag: process.env.FLAG})
        else res.render("home.ejs", {username: username, flag: "no flag for you"})
    } else {
        res.render("unauth.ejs")
    }
})
>
> app.route("/login")
.get((req, res) => {
    if(req.cookies.userData && req.cookies.userData.userID) {
        res.redirect("/")
    } else {
        res.render("login.ejs", {err: false})
    }
})
.post((req, res)=> {
    const request = {
        username: req.body.username,
        password: req.body.password
    }
    const user = users.find(u => (u.username === request.username && u.password === request.password))
    if(user) {
        res.cookie("userData", {userID: user.userID, username: user.username})
        res.redirect("/")
    } else {
        res.render("login", {err: true}) // didn't work!
    }
})
>
> app.get("/logout", (req, res) => {
    res.clearCookie("userData")
    res.redirect("/login")
})
>
> app.listen(3000, (err) => {
    if (err) console.log(err);
    else console.log("connected at 3000 :)");
})
```
From app.js we can see when home is rendered the flag is given as parameter and the real flag is only displayed when `req.cookies.userData.userID === admin.userID` and `req.cookies.userData.username === "admin"`. But we don't know the password or userID for admin. I bruteforced the ID using burp. First login with the given credentials and send the request to intruder. The payload will be all 3 digit numbers and the cookie in base request will be
```
Cookie: userData=j%3A%7B%22userID%22%3A%22§§%22%2C%22username%22%3A%22admin%22%7D
```

Run the sniper attack and the response with correct ID will be of length 2044. Others will be 2038 length.
The userID for admin = 768

flag - `flag{y4m_y4m_c00k13s}`
