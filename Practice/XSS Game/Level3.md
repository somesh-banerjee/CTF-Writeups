# [Level 3: That sinking feeling...](https://xss-game.appspot.com/level3)

Now in this level there is no place for entering anything. When we are changing the photo the url is also changing that means we have 
to manually change the url to run the script.

**index.html**

```
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
 
    <!-- Load jQuery -->
    <script
      src="//ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js">
    </script>
 
    <script>
      function chooseTab(num) {
        // Dynamically load the appropriate image.
        var html = "Image " + parseInt(num) + "<br>";
        html += "<img src='/static/level3/cloud" + num + ".jpg' />";
        $('#tabContent').html(html);
 
        window.location.hash = num;
 
        // Select the current tab
        var tabs = document.querySelectorAll('.tab');
        for (var i = 0; i < tabs.length; i++) {
          if (tabs[i].id == "tab" + parseInt(num)) {
            tabs[i].className = "tab active";
            } else {
            tabs[i].className = "tab";
          }
        }
 
        // Tell parent we've changed the tab
        top.postMessage(self.location.toString(), "*");
      }
 
      window.onload = function() { 
        chooseTab(unescape(self.location.hash.substr(1)) || "1");
      }
 
      // Extra code so that we can communicate with the parent page
      window.addEventListener("message", function(event){
        if (event.source == parent) {
          chooseTab(unescape(self.location.hash.substr(1)));
        }
      }, false);
    </script>
 
  </head>
  <body id="level3">
    <div id="header">
      <img id="logo" src="/static/logos/level3.png">
      <span>Take a tour of our cloud data center.</a>
    </div>
 
    <div class="tab" id="tab1" onclick="chooseTab('1')">Image 1</div>
    <div class="tab" id="tab2" onclick="chooseTab('2')">Image 2</div>
    <div class="tab" id="tab3" onclick="chooseTab('3')">Image 3</div>
 
    <div id="tabContent"> </div>
  </body>
</html>
```

The function ```chooseTab(num)``` is doing the work of changing image. num is directly used in the code. So just by changing the
url to ```https://xss-game.appspot.com/level3/frame#3' onerror="alert()"``` we can get the alert.
