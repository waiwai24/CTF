# Goal

The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.



# Ideas

`cat data.txt`,all are gibberish, so we need to use `strings` to find a printable string in an object file or **binary file**

we konw  "=" is in answer line

enter `strings data.txt | gtep =`

```
=2""L(
x]T========== theG)"
========== passwordk^
Y=xW
t%=q
========== is
4=}D3
{1\=
FC&=z
=Y!m
        $/2`)=Y
4_Q=\
MO=(
?=|J
WX=DA
{TbJ;=l
[=lI
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
>8=6
=r=_
=uea
zl=4
```

 so passswd is:

G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s