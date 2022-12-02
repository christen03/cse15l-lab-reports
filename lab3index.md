# CSE 15L Week 5 Lab Report - Christen Xie  

Welcome back! This lab report will go over the `less` command.

The `less` command is used to display contents of a file or output, but only one page at a time. So if I were to use this command on a large file, such as `chapter 13.4` in 911reports, it would output this: 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/originalless.png?raw=true)

But there are a lot more possible command-line options with this less command that we're going to look at today!

## Option 1: -n/-N

The **-n and -N** command tags are used to modify the line numbers when viewing the text file.  For example, if I'm in my `./technical` directory already and I type in the command:

`less -N government/Media/Annual_Fee.txt`, I would get the following output: 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/annualFeeLineNumbers.png?raw=true)

The **-N** in the command made the line numbers show up. This is extremely useful when viewing many text files, especially if you're editing and need find a line to edit. However, if you're just in it for viewing and don't want line numbers, you can use **-n**.  If I run 

`less -n government/Media/Annual_Fee.txt`, I get the following output: 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/annualFeeNoNumbers.png?raw=true)

It's definitely a lot cleaner of a read. What if you are to run boht of the commands? Like what if my input command were to be

`less -n -N government/Media/Anthem_Payout.txt`, I get the following output: 


![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/anthemNumbers.png?raw=true)

As you can see it's just going to be whichever input is second, so if I inputted `less -N -n government/Media/Anthem_Payout.txt` instead, there would be no line numbers.

## Option 2: -p

The **-p** command is very useful when finding certain patterns of text in a file. You would use it along with a certain pattern and a file to find that text pattern in a file. For example if I inputted 

`less -p "different case" government/Alcohol_Problems/Session2-pdf.txt`, I get this:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/differentcase.png?raw=true)

It's really nice because what it directly finds the pattern of text, so if you're ever looking for a certain keyword inside a text file, you can use **-p**. Here's another example with the input 

`less -p "alcohol screening" government/Alcohol_Problems/Session4-pdf.txt`

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/screening.png?raw=true)

As you can see, I looked for the pattern "alcohol screening" and it was highlighted for me. Now what if you search for a pattern that doesn't exist? What if I input 

`less -p "alcohol screening fjldkfjslkdjflsjfls" government/Alcohol_Problems/Session4-pdf.txt`

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/no_pattern.png?raw=true)

You get a screen that says nothing was found, very useful for if you're looking for certain keywords! A very fast way to filter through files. 

## Option 3 -s

The **-s** command input allows you to squeeze blank lines. For example, if I just open this file without **-s** I get this:

`less government/About_LSC/State_Planning_Special_Report.txt`

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/notusings.png?raw=true)

But if I use **-s**, it turns out:
 
`less -s government/About_LSC/State_Planning_Special_Report.txt`

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/usings.png?raw=true)

It compresses the file and makes it a lot cleaner to read!
This becomes pretty helpful if you combine it with *-N* to make a clean file with lines:

`less -s -N government/Gen_Account_Office/d01186g.txt` which outputs:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/sAndN.png?raw=true)

Of course, if you use it on a file that doesn't have a ton of spaces already, it doesn't do much.

`less -s plos/journal.pbio.0020439.txt` will output: 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab3images/plos.png?raw=true)

which is the same output with or without the -s.


Thanks for reading this week's lab report, it was fun to make :)

**Christen Xie**

