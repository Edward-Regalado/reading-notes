## What is a File? 
- Its a contiguous set of byes used to store data. This data is organized in a specific format and can be anything as simple as a text file or as complicated as a program executable.
Files are composed of 3 main parts: 
1. Header: metadata about the contents of the file (name, size, type)
2. Data: contents of the file as written by the creator or editor
3. End of file (EOF): special character that indicates the end of the file.
## File Paths 
- the path is a string that represents the location of a file and is broken up into three major parts
1. Folder Path: file folder location on the file system where subsequent folders are separated by a forward slash or backslash
2. File Name: name of file.
3. Extension: end of the file path pre-pended with a period (.) used to indicate the file type.
## The double
- dot (..) can be chained together to traverse multiple directories above the current directory. ../../animals.csv
## LIne Endings
- windows uses the CR+LF characters to indicate a new line, while Unix and the newer Mac versions use just the LF character. Pug\r\n
## Character Encodings
- another common problem that you may face is the encoding of the byte data. An encoding is the translation from byte data to human readable characters. 
- The two most common encodings are the ASCII and UNICODE formats. 
- Opening and Closing a File in Python- this is done by invoking the open() built-in function. file = open('dog_breeds.txt'). It's important to remember that it's your responsibility to close the file. You can use a try-finally block or a with statement. The with statement automatically takes care of closing the file once it leave the with block and it allows for cleaner code. 
reader = open('dog_breeds.txt')        with open('dog_breads.txt') as reader:
    try:                        # file processing goes here
      # file processing goes here
    finally: 
      reader.close()
## Text File Types 
- a text file is the most common file that you'll encounter. open('abc.txt') open('abc.txt', 'r')
## Buffered Binary File Types 
- file type that is used for reading and writing binary files. open('abc.txt', 'rb') open('abc.txt', 'wb')
- Iterating Over Each Line in the File - use .readline() method to perform that iteration: 
-with open('dog_breeds.txt', 'r') as reader:
     # Read and print the entire file line by line
     line = reader.readline()
     while line != '':  # The EOF char is an empty string
         print(line, end='')