# [Micro-CMS v1](http://34.94.3.143/ecfe188ca5/)

## Hints:
### Flag0
- Try creating a new page
- How are pages indexed?
- Look at the sequence of IDs
- If the front door doesn't open, try the window
- In what ways can you retrieve page contents?

### Flag1
- Make sure you tamper with every input
- Have you tested for the usual culprits? XSS, SQL injection, path injection
- Bugs often occur when an input should always be one type and turns out to be another
- Remember, form submissions aren't the only inputs that come from browsers

### Flag2
- Sometimes a given input will affect more than one page
- The bug you are looking for doesn't exist in the most obvious place this input is shown

### Flag3
- Script tags are great, but what other options do you have?

## Do it Yourself

## More hints from my side:
### Flag0
- you can access a page in two ways: normal and edit

### Flag1
- Dont forget to try SQLi with edit pages

### Flag2

### Flag3
