# Goal

log into the game using SSH,The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **bandit0**.

The password for the next level is stored in a file called **readme** located in the home directory.



# Ideas

usign cmd

```
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

then enter password `bandit0`.

enter `ls` to list dirctory contents,wo find readme，use  `file readme` to  determine file type,  then `cat readme` to get password to next level.

NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
