# BINF7001_Module1
This repository is to compliment the practical sessions which will take you through basic Linux/unix commands and how to use command line tools. If you find this session a struggle please spend the next week going through the unix tutorial notes in the [Software Carpentry
resources](https://swcarpentry.github.io/shell-novice/aio/index.html) and review your notes from BINF6000 on commandline computing.

Please note, you should insert the relivant information whenever you see `<>`. For example, when you see `$ echo "My name is <name>"` you should use `$ echo "My name is Rhys"`

## Navigating the directory structure

### Printing the current working directory
The full path of the current working directory will be printed to standard output if you use the `pwd` command. 
```
$ pwd
/Users/rhys
```

### Showing the contents of a directory
The `ls` command will list the contents of a directory and print to the screen as standard output.
```
$ ls /Users/rhys
Applications  Movies     bin         Music      Desktop   Downloads
Dropbox       Pictures	 miniconda2  Documents	 Public    miniconda3
```

To list all files with detailed information, use:
```
$ ls -l
```

To list all files in a directory and order by time, use:
```
ls -l -t
```

To list the top 3 lines (2 files and the total)
```
ls -l -t | head -3
```

To list the first 2 lines of files (skipping the size line)
```
ls -l -t | tail -n +2 | head -2
```

To list the unique files using the first 7 characters of file names
```
ls -1 | cut -c1-7 | sort -u
```

To list and use cut to split the text by "_" and takes the first field of each file name
```
ls -1 | cut -f1 -d"_" | sort -u
```

To list files in directory and count lines
```
ls -1 | wc -l
```
	
To list lines in directory and count characters	
```
while read f ; do echo $f | wc ; done < ${FILE}
```

### Making a new directory
The `mkdir` command will create a directory(s)
The `rmdir` command will delete a directory(s)
```
$ cd /home/<user_ID>
$ mkdir week1
$ mkdir week1/seqs
$ cd week1
```

### Changing directories
The `cd` command will allow you to move around your directories

To move into your directory, use:
```
$ cd week1 
```
To move up one level in the directory tree, use:
```
$ cd ../ 
```
To move to the `week1/seqs` directory, use
```
$ pwd
/Users/<user_ID>

$ ls 
week1

$ cd week1/seqs 
```
To return to your home directory, use:
```
$ ls
/Users/<user_ID>/week1/seqs 

$ cd 

$ pwd
/Users/<user_ID>
```

### Moving directories
To move files (can also use for renaming), use:
```
$ mv <Path/To/File/filename> <destination>
```
A similar command can be used for copying files:
```
$ cp <Path/To/File/filename> <destination>
```

## File compression and archiving
The `gzip` command will compress a single-file where the output will typically have the suffix `.gz.`
To compress a file (produces a new file with the `.gz` extension), use:
```
$ gzip <filename>
```
To umcompress a file , use:
```
$ gunzip <filename>
```

The `tar` command will archive a folder where the output will typically have the suffix `.tar.gz`
To create a tar archive, use
```
$ tar -cvzf <New_name>.tar.gz <foldername_to_compress>
```

To extract files from a tar archive, use: 
```
$ tar -xzvf <foldername_to_uncompress>.tar.gz
```

## Creating soft symbolic links
Soft links are created with the `ln` command. To link a file to your current working directory, use:
```
$ ln -s <Path>/<file> <link>
```
Then to verify the new soft link, use:
```
$ ls -l <Path>/<file> <link>
```

## Replacing text
To find and replace text within a file (using LINUX), use:
```
$ sed -i 's;<OriginalText>;<ReplacementText>;g' <file>.txt
```

To find and replace text within a file (using MacOS), use:
```
$ sed -i '' 's;<OriginalText>;<ReplacementText>;g' <file>.txt
```

To rename a large number of files in the same directory all at once, use:
```
$ ls *.fsa
file1_001.fsa	file2_001.fsa	file3_001.fsa	file4_001.fsa	file5_001.fsa
file6_001.fsa	file7_001.fsa	file8_001.fsa	file9_001.fsa

$ for i in *.fsa; do     mv "$i" "${i//.fsa/.fasta}"; done`

$ ls
file1_001.fasta	file2_001.fasta	file3_001.fasta	file4_001.fasta	file5_001.fasta
file6_001.fasta	file7_001.fasta	file8_001.fasta	file9_001.fasta
```
To removed numbers after `_` in a large number of files in the same directory all at once, use:
```
for file in *.fasta; do NEW="`echo $file | awk -F"_" '{print $1}'`.fasta"; mv $file $NEW; done

$ ls
file1.fasta	file2.fasta	file3.fasta	file4.fasta	file5.fasta
file6.fasta	file7.fasta	file8.fasta	file9.fasta
```
