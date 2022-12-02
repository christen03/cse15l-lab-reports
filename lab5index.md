# CSE 15L Week 9/10 Lab Report - Christen Xie  

Welcome back! This lab report will go over using shell scripts to "grade" Java files.

Here, we've created a simple shell script that will take a GitHub repository as an input and run a few checks on it. These checks will ultimately lead to an assigned grade, which will be outputted. To get started, here is an example of the `grade.sh` I wrote, this is what will be used to grade an inputted GitHub repo:


```
rm -rf student-submission
git clone $1 student-submission
cp TestListExamples.java student-submission
cp lib/hamcrest-core-1.3.jar student-submission
cp lib/junit-4.13.2.jar student-submission
cd student-submission
CPATH=".:hamcrest-core-1.3.jar:junit-4.13.2.jar"
if [ -f "ListExamples.java" ]
then
    echo ""
else 
    echo "ListExamples.java not found!!! 0/2"
    exit
fi
javac ListExamples.java 2> err.txt > out.txt 
if [ $? -eq 0 ]
then
    javac -cp $CPATH TestListExamples.java 2> err.txt > out.txt
else
    echo "ListExamples.java cannot be compiled!!! 0/2"
    exit
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples 2> err2.txt > out.txt
if [ $? -eq 0 ]
then
    echo "2/2!!!"
    exit
else
    grep -c "error:" err.txt > result.txt
    cat result.txt
    echo "are wrong, total tests: 2!!!"
    exit
fi
 ```

 To start, we'll host this through Java locally, start by running the command:

 `java GradeServer 2000`

 You can use any port for your server. Once hosted, visit it at `http://localhost:2000`!
 To grade GitHub repos, this link uses a query, like that covered in previous lab reports, so to grade a GitHub repo, the link should be `http://localhost:2000/grade?repo=...` where ... is your GitHub repo link.

 ## Examples

Here are some examples of outputs that are run from inputted repos:
From the following repo: *https://github.com/Faith-Okamoto/list-examples-grader* I go to the following link:
**http://localhost:4000/grade?repo=https://github.com/Faith-Okamoto/list-examples-grader** and here is my result:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab4images/example1.png?raw=true)

Here is another example from the following repo: 



Thanks for reading this week's lab report, it was fun to make :)

**Christen Xie**

