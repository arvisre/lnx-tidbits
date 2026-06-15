# Why **sudo cd** won't get you where you want to: </br>  

Last month, I tried creating a user account "tech1" using the command "usermod". I gave "tech1" **sudo** permissions by making an entry in **/etc/sudoers.d**. </br>  
Logging in as user "tech1", I navigated to **/home** and executed the command **ls -l** which resulted in the following:  
drwx------. 14 as    as    4096 May 19 16:59 as  
drwx------.  3 tech1 tech1   99 May 19 17:33 tech1 </br>  
Just because user "tech1" had permissions to execute **sudo**, I tried to run the command **sudo cd /home/as**, hoping to get into the home folder of **as**. </br>  
But to my surprise, I could not change directory and remained at the same current working directory. </br>  
I researched on this and came across a statement **"The directory of a child process can never affect the parent shell's working directory. This is a fundamental Unix/Linux design principle."** </br>  

