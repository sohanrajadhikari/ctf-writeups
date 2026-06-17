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
