# Lab Report Three: Using Command 'grep'

For the command-line options that I selected, namely 

- `-i`
- `-c`
- `-l`
- `-L`

I used the documentation from `man grep`: [https://man7.org/linux/man-pages/man1/grep.1.html](https://man7.org/linux/man-pages/man1/grep.1.html)

## Command-line Option '-i'

![Picture of command -i](https://migelangel04.github.io/cse15l-lab-reports/LabReport3(1).png)

This is the terminal of me using `grep -i`. This command ignores case distinctions in patterns and input data, so 
that characters that differ only in case match each other. As seen in the image above, we see that the input in the quotation marks are all capitals 
but the command-line option tells `grep` to ignore upper cases and care only about the value. Then this prints all the lines with the given input, ignoring 
capitalization. This is useful for finding certain lines in text files without having to worry about capitalization, for example, when trying to find a name.

## Command-line Option '-c'

![Picture of command -c](https://migelangel04.github.io/cse15l-lab-reports/LabReport3(2).png)

Here we have the terminal using `grep -c`. What `-c` does for `grep` is suppress normal output; instead printing a count of matching
lines for each input file. This goes to every file in the given directory and prints out each LINE NUMBER with the given input. Where as the regular `grep`
command prints out the entire line of the given file, `grep -c` outputs only the line of where the input is for every instance of given file. This is useful 
when trying to locate where something is instead of receiving the content on the line and crowding the terminal.

## Command-line Option 'l'

![Picture of command -l(1)](https://migelangel04.github.io/cse15l-lab-reports/LabReport3(3).png)
![Picture of command -l(2)](https://migelangel04.github.io/cse15l-lab-reports/LabReport3(4).png)

In the images above, I use the command `grep -l`. What `-l` does for `grep` is suppress normal output; instead print the name of each
input file from which output would normally have been printed.  Scanning each input file stops upon first match. This is useful in cases in like the example 
above, where I wanted to find the name "john" in my files and see which files had the name "john".

## Command-line Option 'L'

![Picture of -L](https://migelangel04.github.io/cse15l-lab-reports/LabReport3(5).png)

Similar to the command `grep -l`, what `-L` does is suppress normal output; instead print the name of eachinput file from which no output would 
normally have been printed. This means anywhere where there is no matching for the given string input would give the file where the string does not appear
in it's contents (the opposite `-l`). This is useful in a similar way `grep -l` would be useful.

