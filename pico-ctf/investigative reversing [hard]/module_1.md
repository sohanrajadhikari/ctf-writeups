# Investigative Reversing 1

## Initial Inspection
At a first glance, we have the same problem as the last module, but instead of a single png file, we have 3, titled ``mystery.png``, ``mystery2.png``, and ``mystery3.png``. Again, we still have the same binary file.

Sure enough, while executing the binary file, it still asks for flag.txt. Before moving on to directly disassemble the code like we did at the end of the last module. Let us first check on the other 3 files.

### Strings
Using strings on the files, I found some strings at the end of the file after the image data. Here are the contents corresponding to their respective files.  
- mystery.png : ``CF{An1_3d08c574}``
- mystery2.png : No clear data found in form of text but using ``zsteg`` confirmed that there was around 2 bytes of data after the image data ended. This could be a possible clue as well.
- mystery3.png : ``icT0tha_``

### Executing the file
I executed the file with a blank ``flag.txt`` and the data at the end of the image files doubled. Of course, it was just empty strings but nonetheless, data was actually written, meaning this challange might not be so different from the last one. 

### Analyzing the binary
Alright, instead of messing around with assembly code like last time, I installed a plugin in cutter, ``rz-ghidra`` to analyze pseudocode instead. 

<img width="805" height="518" alt="image" src="https://github.com/user-attachments/assets/2c178a48-a79c-4694-8854-4ce7dd981608" />  

The code is very much readable unlike last time, thank you.

So here's what I found after analyzing for a while:
1. All four files are loaded up.
2. The flag in flag.txt is 26 bytes which is then redestributed through a multitude of ways.
3. I will just show you the code reconstructed with the help of AI.

```
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>

int main(void) 
{
    // Open the source and destination files
    FILE *flag_file     = fopen("flag.txt", "r");
    FILE *mystery_file  = fopen("mystery.png", "wb");
    FILE *mystery2_file = fopen("mystery2.png", "wb");
    FILE *mystery3_file = fopen("mystery3.png", "wb");

    // Safety checks
    if (flag_file == NULL) {
        puts("No flag found, please make sure this is run on the server");
        return 1; 
    }
    if (mystery_file == NULL) {
        puts("mystery.png is missing, please run this on the server");
        fclose(flag_file);
        return 1;
    }

    // Read 26 bytes from the flag file into a buffer
    uint8_t flag_buf[26];
    fread(flag_buf, 1, 26, flag_file);

    // Track a shifting counter character used in mystery2 and mystery3
    char counter_char = flag_buf[3]; 

    // Distribute bytes to the output files
    fputc(flag_buf[1], mystery3_file);
    fputc(flag_buf[0] + 0x15, mystery2_file); // '\x15' is 21
    fputc(flag_buf[2], mystery3_file);
    fputc(flag_buf[5], mystery3_file);
    fputc(flag_buf[4], mystery_file);

    // Loop 1: Indices 6 to 9 (4 bytes)
    for (int i = 6; i < 10; i++) {
        counter_char += 1;
        fputc(flag_buf[i], mystery_file);
    }

    fputc(counter_char, mystery2_file);

    // Loop 2: Indices 10 to 14 (5 bytes)
    for (int i = 10; i < 15; i++) {
        fputc(flag_buf[i], mystery3_file);
    }

    // Loop 3: Indices 15 to 25 (11 bytes)
    for (int i = 15; i < 26; i++) {
        fputc(flag_buf[i], mystery_file);
    }

    // Cleanup and exit
    fclose(mystery_file);
    fclose(mystery2_file);
    fclose(mystery3_file);
    fclose(flag_file);

    return 0;
}
```

This is roughly what the ``mystery`` file does. Now, mostly you can see what remains to be done in order to reverse this.


## Reverse Engineering
Now, onto the fun part. I wrote a python code to reverse this on the original images before I did any tampering.
```
# open all the files

with open("mystery.png", "rb") as f:
        mystery1 = f.read()

with open("mystery2.png", "rb") as f2:
        mystery2 = f2.read()

with open("mystery3.png", "rb") as f3:
        mystery3 = f3.read()

# Load the bytes located at the end of the files
d1 = mystery1[-16:]
d2 = mystery2[-2:]
d3 = mystery3[-8:]

#Declare the flag
flag = bytearray()

# Rearrange the bytes into proper order
flag.append((d2[0]-0x15) & 0xff)
flag.extend(d3[0:2])
flag.append((d2[1] - 0x4) & 0xff)
flag.append(d1[0])
flag.append(d3[2])
flag.extend(d1[1:5])
flag.extend(d3[3:8])
flag.extend(d1[5:16])

#Print the flag
print(bytes(flag))
```

Running this code successfully gave the flag : ``picoCTF{An0tha_1_3d08c574}``.
