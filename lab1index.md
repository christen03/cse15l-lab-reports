# CSE 15L Lab 1 Report - Christen Xie  

Welcome to **CSE 15L!** In this tutorial, we'll be going over remote access and how we can work with files through the terminal! Note that this tutorial asssumes that you are running MacOS.

### Step 1 - Download Visual Studio Code
First, go to the website: *https://code.visualstudio.com/*. There, you'll find instructions on how to download and install Visual Studio Code for your computer. Once you've finished installing and downloading, your screen should look something like this:
![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/vscode.png?raw=true)

### Step 2 - Remotely Connecting

Once you have Visual Studio Code downloaded and open, we can start connecting to the remote computer. To start off, we need to open a new terminal inside VSCode. To do this, on top of your screen you should find a *Terminal* button. Cilck that and a drop-down menu will appear where you will find a *New Terminal* option. Once the new terminal is opened, type in the following command, but replacing the section before **@ieng6.ucsd.edu** with your course-account. 
For this example, we will be using the following command:

`$ ssh cs15lfa22eh@ieng6.ucsd.edu`, it should look like this: 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/ssh-run.png?raw=true)
It will prompt you with a password, which you can then enter. **Don't worry if you don't see anything here when you type, it won't show on your screen, but the computer is taking your inputs!**

Once logged in, your terminal should look something like this:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/remotely-connected.png?raw=true)

### Step 3 - Trying Some Commands

Time to have some fun! There are a variety of commands that you can run now, heres a list of potential examples:

- `cd ~` -> change directory, tilde is the home directory.
- `ls ` -> lists all directories in the working directory
- `ls <directory>` -> lists all directories in a given directory.
- `mkdir (directory name)` -> makes a directory with the given name.

I've run a few commands here to show what some potential outputs could look like: 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/trying-some-commands.png?raw=true)

### Step 4 - Moving Files with `scp`

One of the most important benefits of working remotely is that you can copy files from the remote computer back to your local computer, or vice versa. While there are a variety of ways to do this, we're going to do it with the `scp` command here. For this example, we're going to start in the local computer

Start by typing `logout` into the terminal to logout of the remote computer.

Now in VSCode, we can make a new file through the File -> New File. Fill it out with whatever you want, but in this example, I'm going to be using the following code. 

```
class NameAndLocation{
   public static void main(String[] args) {
        System.out.println("Hi! my name is " + System.getProperty("user.name") + " and my home is 
+ System.getProperty("user.home"));
    }
}
```

The name for this file will be *NameAndLocation.java*, so Ill compile it with `javac NameAndLocation.java`, then run it with `java NameAndLocation`.

When all is said and done, this is what my output looks like:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/java-running.png?raw=true)

Now to copy it over to the remote server computer, we can run the command:
`scp NameAndLocation.java cs15lfa22eh@ieng6.ucsd.edu:~/`
The terminal should output something similar to this:

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/scp-copying.png?raw=true)

Now when we log back into the remote server and run the commands `javac NameAndLocation.java` and `java NameAndLocation` you`ll have the file copied over and runnable in the remote server! 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/scp-copied.png?raw=true)

### Step 5 - Setting up an SSH Key

Now everything we've seen may seem cool and all, but isn't it a little annoying and slow that we have to retype in our password everytime we login or copy a file over? If we want to find a faster method, SSH keys are our solution. This is commonly used in work environments that interact with server code often. To set up a ssh key, we want to logout and start in the local server, so `logout` if you have to! The first command will be:
'$ ssh-keygen`

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/ssh-key-generate.png?raw=true)

It will then ask you a few questions such as which file to save the key in and what you want the passpharse to be. You can just hit enter on both and leave them empty. This will leave the key to get saved in the default file, which in my case is:
`/Users/christenxie/.ssh/id_rsa`
Now that the files are created, we need to copy over a public key from our local computer to the server. So naturally, the first step is to login.
`$ ssh cs15lfa22eh@ieng6.ucsd.edu` and enter your password.
Now that we're in the server, let's make a ssh directory.
`$ mkdir .ssh`. Now we can logout again.
In the local server, we want to copy over the key, so we will use `scp` again. For me, the command is 
`$ scp /Users/christenxie/.ssh/id_rsa.pub cs15lfa22eh@ieng6.ucsd.edu:~/.ssh/authorized_keys`
Make sure you use the path you saved the key in for your first path! It will run the copy for a second: 

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/ssh-key-login.png?raw=true)

However, now after we're done, we can `ssh` and `scp` fully without passwords!

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/ssh-key-loggedin.png?raw=true)

*See? No password required!*

### Step 6 - Optimizing Remote Running

A few tips for optimizing your commands:
1. If you put a command in quotes at the end of an `ssh`, you can simply run the command on the remote server. For example, if you run:
`$ ssh cs15lfa22@ieng6.ucsd.edu "mkdir test"`
Will create a directory called *test* in the remote server!

2. Putting semicolons after each command in a terminal will all you to run multiple commands at once:  

![alt text](https://github.com/christen03/cse15l-lab-reports/blob/main/lab1images/optimize.png?raw=true)

Here, I copied *NameAndLocation.java* into a new file called *NameAndLocation2.java* and compiled it using `javac` in the same command, just split by a semicolon. Then, next command I executed it using `java`

3. The up arrow will allow you to recall commands run before, hitting it once will recall the previous command, two times the second previous, three times third, etc.

## Conclusion

Now that you have all the information to remotely connect to another computer and work with file systems, you're ready to take on CSE 15L! Best of luck!

**Christen Xie**

