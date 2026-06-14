## Nice netcat
Used nc to connect and get the list of numbers. Noticed it looked like ASCII characters so went to Cyberchef, used ``from charcode`` and got the flag.


## Tab, Tab, Attack
Unzipped given file using ``unzip`` and navigated to the end to grab the flag.


## Python Wrangling
Got a file called *ende.py* which contained the code to encrypt or decrypt a file with a passwords.  
Also got *password.txt* and *flag.txt.en*.  
Used ``cat password.txt`` to view and copy the password.  
Used ``python ende.py`` and learned how to use -e and -d flags.  
Finally used ``python ende.py -d flag.txt.en`` and entered the password to get the flag.


## Magikarp Ground Mission
Connected to teh instance remotely through ssh.
`` ssh wily-courier.picoctf.net -l ctf-player -p 64776 ``  
Then navigated through the files to get the keys.
