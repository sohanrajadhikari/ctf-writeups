# Vault Door Series

## Vault Door Training
I was a bit unfamiliar with the Java code but the password at the bottom of the source code made the problem pretty obvious.  
It took me some time to realize that the password should be wrapped up in picoCTF{} but figured out eventually.


## Vault Door 1
Using ``cat`` was sufficient enough to obtain the scrambled password and rearrange it.

## Vault Door 3
I analyzed the code and found that there was some complex code. I wrote a simple python code to reverse engineer the password process and spit out the flag.
```
target = "jU5t_a_sna_3lpm11g54e_u_4_m4r042"
password = [""] * 32

# Reverse Loop 1
for i in range(0, 8):
    password[i] = target[i]

# Reverse Loop 2
for i in range(8, 16):
    password[23 - i] = target[i]

# Reverse Loop 3
for i in range(16, 32, 2):
    password[46 - i] = target[i]

# Reverse Loop 4
for i in range(31, 16, -2):
    password[i] = target[i]

# Combine the characters into the final string
flag_contents = "".join(password)
print(f"picoCTF{{{flag_contents}}}")
```


## Vault Door 4
I used ``cat`` and found that the characters of the password were encoded in ``decimal``, ``hex`` and ``octal`` respectively. It was just a matter of decoding in cyberchef after that!  



## Vault Door 5
Just taking a look at the code was enought to confirm that the code uses ``url-encoding`` followed by ``base64`` encoding. I just had to decode in the reverse order in Cyberchef and get the flag.  


## Vault Door 6
After looking at the code, it was obvious that the encoding used was simple ``hex`` and ``XOR`` with the key being ``0x55``. Same process as the previous one and the flag was obtained.




## Vault Door 7 [Hard]

 
