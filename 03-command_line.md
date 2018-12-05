# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

> > pwd
> > mkdir foldername
> > rm -r foldername
> > touch filename
> > rm filename
> > mv filename1 filename2
> > ls -a
> > cp folder1/filename1 folder/
> >
> >

---

### Q2.  List Files in Unix   

What do the following commands do:  


`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`   

> > `ls` = displays files and folders  
> > `ls -a` = displays all files    
> > `ls -l` = displays the long format of the listing   
> > `ls -lh` = displays the long format and human readable format (print file sizes)    
> > `ls -lah` = displays the long format of all files (including hidden ones) and human readable form     
> > `ls -t` = displays the files, sorted by last modified     
> > `ls -Glp` = displays the files with colorized output, in the long format and foldernames are indicated by slash (/)    


---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> > ls -G  
> > ls -lt  
> > ls -Gp  
> > ls -t  
> > ls -Glht  

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> > `xargs` reads a stream of standard input and converts it into arguments to a command   
> > ls *md | xargs wc  
