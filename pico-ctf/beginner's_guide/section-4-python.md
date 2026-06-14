## Python Wrangling
Got a file called *ende.py* which contained the code to encrypt or decrypt a file with a passwords.  
Also got *password.txt* and *flag.txt.en*.  
Used ``cat password.txt`` to view and copy the password.  
Used ``python ende.py`` and learned how to use -e and -d flags.  
Finally used ``python ende.py -d flag.txt.en`` and entered the password to get the flag.


# PW CRACK SERIES

## PW Crack 1
Looked at the hint.  
``nano level1.py`` to check for the password. Found the password inside the if block.  
Used ``python level1.py`` and supplied the correct password to get the flag.


## PW Crack 2
Used the same concept as last one but the password in the if block was in the *0x..* hexadecimal format.  
Used CyberChef to convert into normal hexadecimal and entered the password to get the flag.


## PW Crack 3
Tried a bit new method for this one. I looked into the *level3.py* file and found somethings interesting.  
I wrote a script of mine own to check for the correct password automatically instead of inputting one by one by hand.
```                               
import hashlib

# copied from level3.py
#hashes the password
def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()

#possible passwords
pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]

#loads the correct hash
correct_pw_hash = open('level3.hash.bin', 'rb').read()

#checks if each password in the list is identical to the correct hash when hashed by hash>
for pw in pos_pw_list:
        if hash_pw(pw) == correct_pw_hash:
                #prints the correct password
                print(pw)
                break
```
This script gave the correct password, which was then used to extract the flag.


## PW Crack 4
For this challange, I used the same script as the last one to find the password but with two changes.  
The ``correct_pw_hash = open('level3.hash.bin', 'rb').read()`` was changed to ``correct_pw_hash = open('level4.hash.bin', 'rb').read()``  
Nothing too dramatic, just changed the 3 to 4.  
Also, the *pos_pw_list* was updated to include all the 100 possible passwords. The script worked, gave the password and the flag was obtained.


##PW Crack 5
The concept was pretty clear. Instead of a pre-defined list, I had to read from a file and check each password in the file against the hash list.  
```
import hashlib

#hashes the password
def hash_pw(pw_str): 
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()

#possible passwords
with open('dictionary.txt', 'r') as file:
    pos_pw_list = file.read().splitlines()

#loads the correct hash
correct_pw_hash = open('level5.hash.bin', 'rb').read()

#checks if each password in the list is identical to the correct hash when hashed by hash>
for pw in pos_pw_list:
        if hash_pw(pw) == correct_pw_hash:
                #prints the correct password
                print(pw)
                break
```
This was the code for this challange. Only change was with possible passwords. All else logic was exactly the same.
