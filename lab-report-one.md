# Lab Report 1 - Remote Access and FileSystem

This will be a guide on how to install Visual Studio Code, connect to a course specfic account and server, and the use of some common commands on the Unix-Shell terminal.

# Step 1: Installing Visual Studio Code

To install VS Code, we can go to the Visual Studio Code [website](https://code.visualstudio.com/) to install it on all major Operating Systems: Linux, Windows, Apple.  
I will go over how to install VS Code using Linux Mint Cinnamon version Venessa (this can also apply to all versions and distributions of Ubuntu) as this is my current operating system but the link provided can go over the other operating systems. 
Open the terminal using `Alt+Ctrl+T`. Next install the WGET if not present.

```
BASH:
$ sudo apt-get update
$ sudo apt-get -y install wget
```

## Step 1.1: Add the repository and key to VS Code
Using the commands writing in the block code below, we will be able to install the APT repository key to our system. 

```
BASH:
$ sudo apt-get update
$ sudo apt-get install apt-transport-https
$ curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
$ sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
```

## Step 1.2 Add the APT repository to Linux
Once the key is installed, add the contents of the repository using:

```
BASH:
$ sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

## Step 1.3 Update the APT and install/run VS Code 
Run the update of the APT package catalog and then install VS Code.

```
BASH:
$ sudo apt-get-update
$ sudo apt-get install code
```

This process will take a bit. After the installation has completed. Run:

```
BASH:
$ code
```

This will appear after the command is run:    
![Image](https://migelangel04.github.io/cse15l-lab-reports/VSCodeIntro.png)  
  

## Step 2: Remotely Connecting  
To remotely connet to a student acccount at UCSD, follow the link here:  

[https://sdacs.ucsd.edu/~icc/index.php](https://sdacs.ucsd.edu/~icc/index.php)

If you need to reset your password for your course specfic account, follow the link [here](https://drive.google.com/file/d/17IDZn8Qq7Q0RkYMxdiIR0o6HJ3B5YqSW/view) and the tutorial listed within the link.  

We will proceed using the CSE15L account but this can apply to a multiple of courses at UCSD. Now that we can have VS Code open from the Step 1.3, we could open the terminal on VS Code (Ctrl or Command+ or use the Terminal --> New Terminal menu option) or we could use the pre-built Linux Terminal as used in Step 1.1 (`Ctrl+Alt+T`). For this demonstration, I will the pre-built terminal but all the same rules apply in the VS Code terminal.  

Using the terminal, type the command below but replace `zz` by the letters of your course-specifc account username.

```
Bash:
$ ssh cse15lsp23zz@ieng6.ucsd.edu
```










