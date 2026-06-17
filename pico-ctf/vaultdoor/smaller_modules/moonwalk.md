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

### SSTV
In the end, I opened the first hint and immediately knew that there was an image file within the .wav file. After that, I researched and found you could decode these images with a SSTV decoder. The image came out upside down but I could find the flag from that pretty easily.
<img width="528" height="417" alt="image" src="https://github.com/user-attachments/assets/66852661-1a68-4961-9075-93b8cb99b455" />

Once again, I tried using steghide with the newly found flag but it was pretty obvious that the steghide was a red herring. Pretty smart, in my opinion. Would have been hard to do this without any hints.


<hr>

## Part 2 [Hard]
Okay, this one is a bit different. There are four different files instead of one. ``message.wav``, ``clue1.wav``, ``clue2.wav``, ``clue3.wav``. I imagine I will have to solve all of the clues in order before approaching the big bad final boss but we'll have to see.

### Exiftool
Exiftool revealed nothing significant except for the fact that all 4 are different in length and are 'unique pieces'.

### SSTV
I don't imagine they would try to pull the same trick twice but you can't be too sure, that is why I scanned all 4 for any hidden images inside them.
1. message.wav - The image came out the same as the last challange, which is immediately a red flag. Sure enough, the final flag was not in the image.
2. clue1.wav - The image had this `` password : hidden_stegosaurus `` which can only mean that something like zteg was used in one of the 4 files and we have to use this passkey to crack it.
3. clue2.wav - The image contained this : ``The quieter you are the more you can HEAR``. I don't understand this at the moment, truly. If I had to guess, I would probably have to lower the volume or do something related to it in this clue.
4. clue3.wav - To be honest, the image is a little blurry so I don't understand the full text. I can guess what is being said is :  `` Alan Eleaser the FutureBoy``. Again, I suspect this to be just a bait.

### Steghide
So, I tested the pasphrase for message.wav. 
<img width="521" height="43" alt="image" src="https://github.com/user-attachments/assets/f44d2caf-b178-4733-8b4b-ebf8e7adea25" />
Now, using cat, the flag was found easily. Meaning, the only clue needed was the clue1.   

To be honest, the first one deserved the "hard" tag a lot more than the second one. But that may just be because of the second one buiding on the first one.
