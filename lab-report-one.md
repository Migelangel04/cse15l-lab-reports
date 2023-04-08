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
Using the commands writing in the block code below, we will be able to install the APT repository key to our system. An APT repository is a collection of deb (debian) packages with metadata that is readable by the apt-* family of tools, namely, apt-get.

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
Run the update of the APT package catalog and then install VS Code. The update will give your the latest version of VS Code and the install will install it to the computer.

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
$ ssh cs15lsp23zz@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type 'yes' in the terminal to contiune after this message appears. This will prompt a password verfication where you will type the course specific password that came with your course specfic username. This should be the password you made when reseting your account. Once you have your password, save it as it will be used to log into the UCSD Linux terminals.

The terminal should look something like this after login: 

![Image](https://migelangel04.github.io/cse15l-lab-reports/UCSDTerminalCSE15L.png)

## Step 3: Terminal Commands

There are multitude of commands that the Linux Kernal utilizes however the ones that have been discussed in class so far are `cd`, `ls`, `pwd`, `mkdir`, and `cp`. These commands are vital in trying to navigate the file system using the terminal. Here I am demonstrating the use of some of these commands on the UCSD Linux servers using the terminal from the pervious step:  

![Image](https://migelangel04.github.io/cse15l-lab-reports/TerminalCommands.png)

This concludes the lesson!












