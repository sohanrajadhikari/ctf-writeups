## Enhance!
The svg didn't really show the flag at first. Downloaded inkscape to manage svg more carefully.  
Saw that there was a "Text Path". Extracted the flag from there.



## Big Zip
Downloaded the file, unzipped it, used ``grep "picoCTF" -r`` and boom! Got the flag.



## Vault Door Training
I was a bit unfamiliar with the Java code but the password at the bottom of the source code made the problem pretty obvious.  
It took me some time to realize that the password should be wrapped up in picoCTF{} but figured out eventually.



## keygenme-py
I looked at the code first. I found out that the code wanted me to enter a license key (most likely the flag) and I would have to reverse engineer how the flag is made.  
What I did is first look at how the key was constructed. The key consisted of three parts :
- ``picoCTF{1n_7h3_kk3y_of_``
- ``xxxxxxxx``
- ``}``
Basically, my job was then to figure out what the eight digits in the 2nd part of the key was.

Firstly, I found out that a hashing module ``hashlib`` was used and we could use it's help in finding the key.  
The key was generated with the username with code like ``hashlib.sha256(username_trial).hexdigest()[4]`` where each character of the ``xxxxxxxx`` corresponded to a fixed character of the hexdigest output. Namely the order went as :  
``4 5 3 6 2 7 1 8``  
For this, I wrote a quick script that printed the hexdigest of the username_trial.
```
import hashlib
username_trial = "BENNETT"
bUsername_trial = b"BENNETT"

x = hashlib.sha256(bUsername_trial).hexdigest()
print(x)
```
Initially, I forgot that the arrays start with 0 and not 1 and ended up with this key : picoCTF{1n_7h3_kk3y_of_co68a4ba} which was incorrect.  
Finally, I reordered the characters in the correct format and got the final key : `` picoCTF{1n_7h3_kk3y_of_08c46aa4} ``



## buffer overflow 0
At first, I had no idea what to do. I looked inside the code of ``vuln.c`` and observed that the buffer limit for buffer was 64. So, I connected with help of ``nc`` with the instance and overloaded the buffer with more than buffer size and got the flag.
