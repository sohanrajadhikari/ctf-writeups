## Static ain't always noise
Looked at the contents of ``ltdis.sh`` file and made it executable. Executed the file and used it to parse the binary content and find the flag.


## Strings it
Downloaded the strings file. Went to terminal and used ``cat`` to list the contents.  
Discovered hint about the strings function. Used ``man strings`` to find out about strings.  
``strings`` is a useful tool to list all the printable strings in a file.  
Used ``strings`` to find but couldn't find at first. Used ``-d`` and ``-a`` flags as well.  
Got stuck, couldn't find the flag.  
Used find, and then found it.


## Plumbing
Connected to the instance using netcat and stored the output in flags.txt.
```
nc fickle-tempest.picoctf.net port > flag.txt
```
Then scanned the file for the flag.
```
grep "picoCTF" flag.txt
```
