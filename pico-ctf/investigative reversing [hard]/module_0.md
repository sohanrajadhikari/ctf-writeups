## Investigative Reversing 0

We are given two files : ``mystery.png`` and ``mystery`` bin file.

Right off, the bat, opening the png doesn't really give anything except a question : "Where did the flag go?"

### Cat
Using ``cat`` on mystery.png, I found a string right at the end of the file : picoCTK�k5zsid6q_6099dfbd}. Now, this might or might not be the flag but the format matches. Just the CTF is changed to CTK and the { is changed to an unrecognizable character. Maybe a substitution has been done on select characters.

### Executing the file
The mystery binary file might be executable, so I used ``chmod +x mystery`` to make the file executable and executed it. The output was a bit confusing.
<img width="498" height="56" alt="image" src="https://github.com/user-attachments/assets/51ab6040-fe7e-4a7d-826c-4f15669893a9" />

### Strings
Looking at the output of `` strings mystery | less ``, I found a few strings that were quite suspicious : mystery.c, flag.txt, mystery.png. Something can be inferred from this that the ``mystery`` file is compiled from ``mystery.c`` and output or input might be ``flag.txt``.

### Zsteg
Using ``zsteg`` on mystery.png yielded the exact same results as in the cat one.
<img width="669" height="102" alt="image" src="https://github.com/user-attachments/assets/d7466dc9-ad3e-4754-bd56-01b2cd146f56" />  
picoCTK.k5zsid6q_6099dfbd}

### Executing the file again
I got an idea by seeing the flag.txt. I created a file called ``flag.txt`` and pasted the previous flag looking text(picoCTK.k5zsid6q_6099dfbd})   
Using ``cat`` again, I found that a new flag like text has been generated again at the end. ``picoCTP3p:xni;n_6099dfbd}``  
Doing this 4-5 times revealed that a new flag was generated each time but not "picoCTF{...}" format. Maybe writing a script to rerun this step until a "picoCTF" flag is generated would make sense?
Wait, across all the flags generated, the first part : ``picoCT`` and last part : ``_6099dfdb`` remain the same but the middle part is being courrupted, probably through an algorithm.


## Cutter
I tried to view the assembly code using ``objdump`` but couldn't understand any of it. So, I thought it would be better to just open a decompiler like Cutter(rizin-cutter).  

<img width="910" height="510" alt="image" src="https://github.com/user-attachments/assets/3baaf0e3-bf15-4069-ae4b-510143f451e6" />

Since, I'm not an assembly genius, I used AI to analyze what the assembly code really did. Here's what I found out :  
1. The first 6 characters,([0]-[5]) remain unchanged.
2. From [6] to [14], each byte is shifted/incremented by +5.
3. [15], the byte is shifted left, i.e., -3.
4. Rest of the bytes are normal.


## Reverse Engineering
Since I know how the flag is generated now, I will just have to take the very first flag, shift its bytes and be done with it.

```
#open the file "mystery.png"
with open("mystery.png", "rb") as f:
        data = f.read()

# read the last 26 bytes from the file
encoded = data[-26:]


flag = bytearray()

flag.extend(encoded[:6])
flag.extend((b-5) & 0xff for b in encoded[6:15])
flag.append((encoded[15] + 3) & 0xff)
flag.extend(encoded[16:26])

print(bytes(flag))
```
Finally, the flag was found : picoCTF{f0und_1t_6099dfbd}

This challange is truly deserving of its ``hard`` tag.
