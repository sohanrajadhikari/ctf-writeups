## Sleuthkit Intro
The ``mmls`` command after unzipping through ``gzip -d filename`` was enough.

## Disk, disk, disk, Sleuth!

### Part I 
I don't know if I did it the right way, but I used just two commands in the end.  
I messed about a bit but it didn't lead to anywhere. So, what I did is these three commands that basically spit out the flag.   
```
dd if=input_file of=output_file.img
srch_strings -o offset output_file.img > find.txt
grep "picoCTF" find.txt
```

### Part II
Downloaded the file, didn't know how to search for files at first. Used google to find the compound commands format.
```
srch_strings -r -o offset disk.img | grep "down_at_the_bottom.txt"
icat -o offset disk.img inodenumber
```
The first command gave the inode and the second one gave the flag.


## Sleuthkit apprentice
Looked through all the folders but the usual ``grep`` and ``srch_strings`` commands didn't work.  
Went to autopsy, sorted the files by categories and stumbled upon a file wit "flag" in it's name. Used ``icat`` to list the file's contents and found the flag.
