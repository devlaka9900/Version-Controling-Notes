ls — lists files and folders
cd — changes the current directory
cat — displays the contents of a file
wc — counts lines, words, and characters
| pipe — sends the output of one command as input to another command

*** ls ***
*** cd ***
*** cat ***
    - The cat command is used to display the contents of a file in the terminal.
    - Ex cat file1.txt
        * This command prints the content inside file1.txt.
        * If file1.txt contains simple text, that text will appear directly in the terminal.
*** wc ***
    - command means word count. It can count lines, words, bytes, and characters in a file.
    - To count only the number of words, we use the -w flag.
    - Ex wc -w file1.txt
        * output 181 file1.txt
    - This means file1.txt contains 181 words.
*** | ***
    - A pipe is written using the vertical line symbol:
    - Pipes allow us to pass the output of one command as the input to another command.
    - ls | wc -w
        * ls lists the files in the current directory.
        * The pipe | sends that output to the next command.
        * wc -w counts the number of words from the output.

# Counting Words in a File Using Pipes
cat file1.txt | wc -w
    - cat file1.txt displays the contents of file1.txt.
    - The pipe sends that text to wc -w.
    - wc -w counts the number of words.
    - Output: 181

# Counting Words from Multiple Files
cat file1.txt file2.txt | wc -w
    - cat file1.txt file2.txt combines and displays the contents of both files.
    - The pipe sends the combined text to wc -w.
    - wc -w counts the total number of words from both files.


