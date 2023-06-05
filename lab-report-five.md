# Lab Report 5: Debugging Scenario & Lab Reflection

## Part 1: Debugging Scenario

`Student: Initial Question`

Hello, I am currently running Linux Mint Cinnamon using Firefox as my main browser and using the built in terminal on my laptop
that runs near identical to a Mac OS Terminal. I am running into an issue on my testing for Lab 7, ListExamples.java and ListExamplesTests.java. Below I have the screenshots of my errors when running the tests, my current working directory, the script for test.sh, and the code for ListExamples.java. The terminal tells me that I messed up on the comparison of the list elements at the given index but I do not know how this is since we need to compare the elements.

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabR5(1).png)

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabR5(2).png)

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabR5(3).png)

`TA/IA/Professor: Initial Response`

Hi! Thank you for your query. It looks like your file system is good operating order and everything is where it should be however, what is appears is that the issue shown by your test is indeed valid within the file ListExamples.java. Remember this merge function takes in a "List<String>" which means that each element is a String type (which is an refernce type). Reference types cannot be compared using >, <, ==, >=, and <=. Instead, I recommend using the s1.compartTo(String s2) comparison for in the first while loop if statement. Where you compare "list1.get(index1) > list2.get(index2)". Also as a note, check the two while loops at the bottem of the page, they seem to have improper comparisons.

`Student: 2nd Response`

Thank you for the solution! I completely forgot that comparison do not work for Strings as they do with ints and doubles lol. Also I did address the suggestion for the bottem two while loops in ListExamples.java. However,I still have issues with the tests.

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabR5(4).png)


`TA/IA/Professor: 2nd Response`

Looking at the tests, it appears that one of your tests passed whilst the other failed. The failure appears to be the JUnit comparaison. You may have a typo within your ListExamplesTests.java file or have it incorrectly step up because on my end, your ListExamples.java file seems to be in working order based on the solutions on our side. You can send a screenshot of your ListExamplesTests.java file or you can attempt to find the issue on your own. Whatever works best for you :).

`Student: Final Response`

Ah thank you for the recommendation. I looked over the file and saw a typo in my tests. I addressed it and my tests have all passed. Thank you very much once again!

![Image](https://migelangel04.github.io/cse15l-lab-reports/LabR5(5).png)

`TA/IA/Professor: Final Response`

No problem, if you have anymore bugs feel free post them!

## Lab Reflection

There are two equally interesting things I learned in the second half of this course. The first was the introduction and use of the bash script. This simplifies the process of writing commands as we can simply type out `bash <file.sh>` and have an entire sequence of commands put out in an instant. The second is the use of loops within said bash scripts. The combination of these two makes it so I can potientially automate my entire system with a few clicks. I will definitely learn more about these outside of this classroom so I can be a more efficent programmer.



