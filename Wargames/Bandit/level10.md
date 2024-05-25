# Goal

The password for the next level is stored in the file **data.txt**, which contains base64 encoded data



# Ideas

`cat data.txt`:
VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==

"==", it appear it is encode by base64:

`base64 -d data.txt`:
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

