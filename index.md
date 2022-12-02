# CSE 15L Week 7 Lab Report - Christen Xie  

Welcome back! This lab report vim to edit text files.
As a brief overview of vim, it's a very powerful text editor that can be run straight in your terminal! It can open a variety of files and is very versatile. Today, we'll be going over some uses and commands.

## Section 1 - Replacing text in vim

In this first example, we'll be taking a look at `DocSearchServer.java`. Here's a preview of the file:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab4images/doc.png?raw=true)

It's not quite the whole file, but it shows the parts that we need. The task today is to change the parameter, `start` (and thus all variables `start`) to `base` using vim. The method to be edited is `getFiles`.

There's a pretty cool command we can use and here the breakdown:
`:%s/` will search the file for any text pattern coming after the `/`. so `:%s/hello` will serach the file for hello. 
If we include another text pattern like `/hi` after this command, we can replace all instance of the first text pattern with the second. so 
`:%s/hello/hi` will replace all instances of hello in the files with hi.
Then, adding a `\gc` at the back will ask for confirmation before converting any string. So here, since we want to only alter the text in getFiles, we want to make sure we're not touching other methods, so I'm running the command:

`:%s/start/base/gc`

This will ask me if I want to replace each instance of `start`, as shown here: the cursor will jump to the first instance of start.

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab4images/edits.png?raw=true)

The first 3 I will input `y` for yes, since they are part of the `getFiles` method, but since the last `start` is in a whole other method, I input `n` for no. (So `y` three times, then `n` once) Now look at our new method!:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab4images/edited.png?raw=true)

Remember to `:wq` to save and exit!

## Section 2 - Vim vs VSCode

Obviously, another amazing text editor is VSCode, it's colorful, fun, and shows compiler errors. However, it can get really slow and annoying when running programs remotely. For this section, I decided to time myself making this same `DocSearchServer.java` edit and running it on VSCode and on Vim.

### VSCode

For VSCode, the whole process took me about 7 seconds to make the edits, as I just hit `CMD+F`, then searched for `start` and replaced it with `base`. Then came the difficulties. I had to `scp` the file to the remote server, then log on to the remote server, then run it which added about another 15 seconds. It ended it a total of about **22** seconds.

### Vim

For Vim, since I was already logged it, it was very easy. I just typed in the command `:%s/start/base/gc`, and the edit was done. I typed in `:wq`, and then ran the test and it was all done. The whole process took me about **5** seconds.

### Summary

Overall, while I do think Vim is cool, I'm not too familiar with the commands, and currently, I'm willing to take the 15 seconds of being irritated for a cleaner, and more visual text editor. I love being able to move my cursor around my code and use basic mac commands to edit my code, as well as easily spot compiler errors. But that's just me right now, as I get more used to Vim, I'm sure things will change. 

Thanks for reading this week's lab report, it was fun to make :)

**Christen Xie**

