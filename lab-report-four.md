# Lab Report Four: Git and GitHub Using Terminal/Vim

## Step 1: Login to IENG6 & Clone Repository

Using the ssh key from lab 7, we logged into ieng6 without using the ieng6 password for the course specfic account and from here I went to [GitHub](https://github.com/) and cloned the repository using the ssh link.

![Image](https://migelangel04.github.io/cse15l-lab-reports/Lab4(1).png)

The image above shows the process in the terminal and the keys used are: 

`ssh cs15lsp23pe@ieng6.ucsd.edu <enter> git clone git@github.com:Migelangel04/lab7.git <enter>`

## Step 2: Failed Testing

Directly after Step 1, we entered the following commands: 

`cd lab7 <enter> javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java <enter> java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests <enter>` 

which results in the image below

![Image](https://migelangel04.github.io/cse15l-lab-reports/Lab4(3).png)

As we can see, we typed in the commands to run JUnit tests within our `ListExamplesTests.java` file and received an error stating we have an error in our code. To fix said issues, we move onto Step 3.

## Step 3: Edit Code to Fix Errors

The errors we had was in the file `ListExamples.java` so to address these issues, we used the following keys after Step 2: 

`vim ListExamples.java <enter>` which takes our terminal to vim and lets us continue our editing. In Vim, we will use keys: `<i>`to enter insert mode and `<h><h>` ... `<h>` until we reach the last while loop within the file `ListExamples.java` as shown:

```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    >>>while(index2 < list2.size()) {
      result.add(list2.get(index2));
      // change index1 below to index2 to fix test
      index1 += 1;
    }
    return result;
  }


}
```

From `>>>` that is highlighted in the code above, we press 

`<h> <h> <h> <right arrow> <right arrow> <right arrow> <right arrow> <right arrow> <right arrow> <backspace> <2> <esc> <:wq> <enter>`

to save edit the mistake in our code above which is change the variable name `index1` to `index2` since we are trying to increment the current index of `list2`. 

This process encompassed the entire process of going into vim to edit our file and then do the `<esc> <:wq> <enter>` sequence to save and quit vim, thus finising the edits necessary to fix our code.

## Step 4: Running Tests with Saved Changes

After we exit vim, we are taken back to our terminal and from the terminal we enter the keys: 

`javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java <enter> java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests <enter>` 

as done in Step 2, however now with our changes. Instead of failed tests, we are shown that tests passed:

![Image](https://migelangel04.github.io/cse15l-lab-reports/Lab4(5).png)

## Step 5: Commit and Push changes to GitHub

Being that we have our GitHub account linked to our terminal from Lab 7, we will now commit and push the changes we made to our GitHub account. From the terminal linked to our ieng6 server, we will use the sequence of keys and commands as follows: 

`git add .` since we are currently in the `lab7` directory and our files are within this directory (`.` represents the current directory) and then `git commit` to enter vim and add a message to our commit. In vim we enter the sequence, `<i> This is my first commit and push <esc> <:wq>` and then `git push` from our terminal. We have sucessfully updated our repository from the terminal as demonstrated and shown: 

![Image](https://migelangel04.github.io/cse15l-lab-reports/Lab4(6).png)

Within GitHub, we have sucessfully updated our repository and the changes are now available to be seen by anyone who has access to the repository.



