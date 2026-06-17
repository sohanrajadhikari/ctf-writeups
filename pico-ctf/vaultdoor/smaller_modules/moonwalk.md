# m00nwalk

## Part 1
Right off the bat, the audio message threw me in for a loop. First, I played it to see if anything could be found. Nothing there, just some irritating sharp noises. Next, I ran ``grep "picoCTF"`` on it to see if something could be done. No luck there either. Then, I had a few ideas about which direction I could take this.

- Maybe the audio file had something hidden that could be shown by exiftool
- Maybe could contain morse code?
- Maybe the audio visualizer could show something, maybe a secret code or a figure.
- Maybe changing the extension or something like a hidden file inside the file could reveal the flag.
- Maybe the audio can be slowed, fastened, or something to do with the pitch that can reveal the flag.
- Maybe there could be link inside the file somewhere.

Keeping these options in mind, I tried all of them one by one.  

### Exiftool:
<img width="490" height="293" alt="image" src="https://github.com/user-attachments/assets/a178977f-44be-4d46-924e-7e248a702761" />  
Nothing obvious was obtained from there.

### Morse Code
Listening to the audio, I thought maybe the audio could be something like morse code. Using an online converter, I found nothing.  
<img width="495" height="328" alt="image" src="https://github.com/user-attachments/assets/cea44568-7117-4645-9a3e-dacb4e173ba4" />  
This idea could be revisited later though.


### Audio Visualizer
<img width="814" height="497" alt="image" src="https://github.com/user-attachments/assets/c199a3f5-6ca5-4a7a-9b47-39249e70a1b2" />  
Seeing the audio waveform didn't give much clue either. Maybe slowing down would provide something.

### Steghide
I remembered about this tool and executed ``steghide --extract -sf message.wav`` immediately which then prompted for a passphrase. Good news : The data definitely hides inside the file. Bad news : I don't know how to extract the passphrase.   
I tried a bruteforce attack immediately but couldn't be cracked with ``rockyou.txt``
<img width="441" height="84" alt="image" src="https://github.com/user-attachments/assets/dbf11deb-7fed-4029-8010-f485138f37a7" />
