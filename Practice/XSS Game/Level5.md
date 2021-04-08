# [Level 5: Breaking protocol](https://xss-game.appspot.com/level5)

This is a bit tricky if you don't know the fact that writing ```javascript:alert(1)``` in url bar can give alert.

This is one of the source code
**signup.html**
```
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>
 
  <body id="level5">
    <img src="/static/logos/level5.png" /><br><br>
    <!-- We're ignoring the email, but the poor user will never know! -->
    Enter email: <input id="reader-email" name="email" value="">
 
    <br><br>
    <a href="{{ next }}">Next >></a>
  </body>
</html>
```

Here we can see the ```Next``` is redirecting to somewhere. If we change to value of next from url then we will get the desired output.

So the url will be ```https://xss-game.appspot.com/level5/frame/confirm?next=javascript:alert(1)```
