# Why **sudo cd** won't get you where you want to: </br>  

Last month, I tried creating a user account "tech1" using the command "usermod". I gave "tech1" **sudo** permissions by making an entry in **/etc/sudoers.d**. </br>  
Logging in as user "tech1", I navigated to **/home** and executed the command **ls -l** which resulted in the following: </br>  
drwx------. 14 as    as    4096 May 19 16:59 as  
drwx------.  3 tech1 tech1   99 May 19 17:33 tech1 </br>  
Just because user "tech1" had permissions to execute **sudo**, I tried to run the command **sudo cd /home/as**, hoping to get into the home folder of **as**. </br>  
But to my surprise, I could not change directory and remained at the same current working directory. </br>  
I researched on this and came across a statement **"The directory of a child process can never affect the parent shell's working directory. This is a fundamental Unix/Linux design principle."** </br>  

## What this really means? </br>  
In the file, 006_bash-basic-concept01.md, I learnt how the **Shell (bash)** calls the **fork()** system call, creates a clone **Child Process**, the **Child Process** takes care of the tasks while the **Shell** calls the **wait()** system call, and finally the **Child Process** completes the tasks and exits with an **exit code**. </br>  

## CASE 1: Why this won't work for sudo cd: </br>  
1. When I execute **sudo cd** the **Shell** calls the **fork()** Kernel System Call and creates a clone **Child Process**.  
2. The **Child Process** has to now look for **sudo**, searches the **PATH** variable and finds the command at **/usr/bin/sudo**.  
3. Now the **Child Process** becomes **sudo**.  
4. Now this **Child Process** creates another **Child Process** to find the command **cd** and carry-on with the task.  
5. The problem is, the command **cd** is a Shell **built-in** and cannot be found in a directory like the commands sudo, find, or ls.  
6. Owing to this reason, the second **Child Process** exits - because it does NOT know where to find **cd**.  
7. Following this, the first **Child Process (sudo)** also exists.  
8. Now that both the **Child Processes** have exited, the parent **Shell** processes that has been in **wait()** resumes and prints a new prompt.  
9. Ultimately, we have not changed to any directory.

## CASE 2: What is **cd** was an external command: </br>  
1. If the command **cd** was an external command, all of the 1-5 points mentioned in CASE 1 will happen.  
2. The **Child Process** will find **cd** in some directory and then will become **cd**, and change to the directory in the argument.
3. But none of these tasks are going to have any effect on the parent **Shell** because, the parent **Shell** is going to come out of **wait()** and print a new prompt.

**So both CASE 1 and CASE 2 are not going to give me the expected outcome.** </br>  
These are the reasons why **sudo cd** is not going to work.  
