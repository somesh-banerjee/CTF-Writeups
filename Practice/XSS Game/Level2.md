# [Level 2: Persistence is key](https://xss-game.appspot.com/level2)

In this level just writing a script tag in the input will not work beacause the message is being posted through a table and script wouldn't work here easily.

**index.html**
```
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
 
    <!-- This is our database of messages -->
    <script src="/static/post-store.js"></script>
   
    <script>
      var defaultMessage = "Welcome!<br><br>This is your <i>personal</i>"
        + " stream. You can post anything you want here, especially "
        + "<span style='color: #f00ba7'>madness</span>.";
 
      var DB = new PostDB(defaultMessage);
 
      function displayPosts() {
        var containerEl = document.getElementById("post-container");
        containerEl.innerHTML = "";
 
        var posts = DB.getPosts();
        for (var i=0; i<posts.length; i++) {
          var html = '<table class="message"> <tr> <td valign=top> '
            + '<img src="/static/level2_icon.png"> </td> <td valign=top '
            + ' class="message-container"> <div class="shim"></div>';
 
          html += '<b>You</b>';
          html += '<span class="date">' + new Date(posts[i].date) + '</span>';
          html += "<blockquote>" + posts[i].message + "</blockquote";
          html += "</td></tr></table>"
          containerEl.innerHTML += html; 
        }
      }
 
      window.onload = function() { 
        document.getElementById('clear-form').onsubmit = function() {
          DB.clear(function() { displayPosts() });
          return false;
        }
 
        document.getElementById('post-form').onsubmit = function() {
          var message = document.getElementById('post-content').value;
          DB.save(message, function() { displayPosts() } );
          document.getElementById('post-content').value = "";
          return false;
        }
 
        displayPosts();
      }
 
    </script>
 
  </head>
 
  <body id="level2">
    <div id="header">
      <img src="/static/logos/level2.png" /> 
      <div>Chatter from across the Web.</div>
      <form action="?" id="clear-form">
        <input class="clear" type="submit" value="Clear all posts">
      </form>
    </div>
 
    <div id="post-container"></div>
 
    <table class="message">
      <tr>
        <td valign="top">
          <img src="/static/level2_icon.png">
        </td>
        <td class="message-container">
          <div class="shim"></div>
          <form action="?" id="post-form">
            <textarea id="post-content" name="content" rows="2"
              cols="50"></textarea>
            <input class="share" type="submit" value="Share status!">
            <input type="hidden" name="action" value="sign">
          </form>
        </td>
      </tr>
    </table>
 
  </body>
</html>
```

**post-store.js**

```
/*
 * Objects to implement a client-side post database.
 */
 
function Post(message) { 
  this.message = message;
  this.date = (new Date()).getTime();
}
 
function PostDB(defaultMessage) {
  // Initial message to display to users
  this._defaultMessage = defaultMessage || "";
 
  this.setup = function() {
    var defaultPost = new Post(defaultMessage);
    window.localStorage["postDB"] = JSON.stringify({
      "posts" : [defaultPost]
    });
  }
 
  this.save = function(message, callback) {
    var newPost = new Post(message);
    var allPosts = this.getPosts();
    allPosts.push(newPost);
    window.localStorage["postDB"] = JSON.stringify({
      "posts" : allPosts
    });
 
    callback();
    return false;
  }
 
  this.clear = function(callback) {
    this.setup();
 
    callback();
    return false;
  }
 
  this.getPosts = function() {
    return JSON.parse(window.localStorage["postDB"]).posts;
  }
 
  if(!window.localStorage["postDB"]) { 
    this.setup();
  }
}
```

But looking at the source code we can see that some other html tags will work here like img tag and by using this we can run a script.
For example we give a invalid source for image than run alert() in onerror attribute. This defenitely run the alert.

Therefore we will put the following as post to run script
```<img src=x onerror="alert()">```
