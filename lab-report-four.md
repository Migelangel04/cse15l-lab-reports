# Lab Report Four: Git and GitHub Using Terminal/Vim

## Step 1: Login to IENG6 & Clone Repository

Using the ssh key from lab 7, we logged into ieng6 without using the ieng6 password for the course specfic account and from here I went to [GitHub](https://github.com/) and cloned the repository using the ssh link.

![Image](https://migelangel04.github.io/cse15l-lab-reports/Lab4(1).png)

The image above shows the process in the terminal and the keys used are: `ssh cs15lsp23pe@ieng6.ucsd.edu <enter> git clone git@github.com:Migelangel04/lab7.git <enter>`

## Step 2: Failed Testing

Directly after Step 1, we entered the following commands: `cd lab7 <enter> javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java <enter> java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests <enter>` which results in the output below.

![Image](https://migelangel04.github.io/cse15l-lab-reports/Lab4(3).png)

As we can see the tests have failed due to error in the code.

## Step 3: Edit Code to Fix Errors

The errors we had was in the file `ListExamples.java` so to address these issues, we used the follow keys after Step 2: `vim ListExamples.java <enter>` which takes our terminal to vim and


