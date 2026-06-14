## Wave a flag
Mistakenly used cat and found the flag.  
Tried the correct way. Forgot the chmod syntax and used the hints for help.  
Used ``chmod +x filename`` and executed the file to get the flag.


## Tab, Tab, Attack
Unzipped given file using ``unzip`` and navigated to the end to grab the flag.

## Insp3ct0r
Opened the webpage, opened the inspect tab.  
Got 1/3rd of the flag from the direct inspect page. Went to network tab and got links to js and css pages.  
Navigated to the remaining pages and collected the full flag.

## Strings it
Downloaded the strings file. Went to terminal and used ``cat`` to list the contents.  
Discovered hint about the strings function. Used ``man strings`` to find out about strings.  
``strings`` is a useful tool to list all the printable strings in a file.  
Used ``strings`` to find but couldn't find at first. Used ``-d`` and ``-a`` flags as well.  
Got stuck, couldn't find the flag.  
Used find, and then found it.


## First Grep
Used Grep to find the picoCTF pattern for the flag
```
grep "picoCTF" file

```


## where are the robots
Got stuck while inspecting the page.  
Went to /robots but found nothing. After sometime, went to /robots.txt, got the link and followed to capture the flag.
