## Packets Primer
All it takes is opening the file with wireshark and analyzing the packets. Nuff said!
<img width="905" height="427" alt="image" src="https://github.com/user-attachments/assets/4170cd32-4266-4fb1-9a72-d5f34d9438c2" />


## Wireshark doo dooo do doo...
Was a bit of a problem at first, didn't know how to navigate such a large number of packets but learned about streams eventually and found a string that looked suspicously like a flag. Put it in cyberchef, used the ROT13 and got the falg.


## Trivial Flag Transfer Protocol
This one was the hardest by far! Probably due to my inexperience with wireshark. I looked at the packets for a while before finding out that some files were donwloaded throughout the transfer but couldn't find out how to extract it. Searched for a while and found out about the export option.  
After exporting all the files, the ``program.deb`` was used to install ``steghide``. After decrypting the message in ``plan``, using steghide to extract the flag using the password was pretty simple.
