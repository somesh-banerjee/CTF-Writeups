[**Problem**](https://ctflearn.com/challenge/195)   (Medium,Forensics)

We just got one jpg file of oreo and got nothing by using ```file``` or ```strings``` command.

- Using ```binwalk''' we found that there is a rar file with the jpg file.

- To get the rar file use ```foremost```

    ```foremost -v oreo.jpg```
    
- to unrar use ```unrar x filename.rar```

- Inside the hidden file you will get another jpg, then using ```strings``` get the flag.
