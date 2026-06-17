# How the built-in command **cd** works: </br>  
Although I was aware that **bash** commands are categorised as **external** and **builtin**, I did not have the clarity how they worked. </br>  
The concepts mentioned in **006_bash-basic-concept01** and **007_why-sudo-cd-wont-work** helped me gain an overview of how the **Shell** treats builtin and external commands. </br>  

When I execute an external command such as **find**, the **Shell (bash)** calls the **fork()** system call, creates clone **Child Process**, the **Child Process** checks the **PATH** variable
to locate the **/usr/bin/find** executable, then the **Child Process** makes another system call and becomes the **find** program, carries out the task, prints the output, and exits (exit code). The **parent process** that was in **wait()** all this long, wakes up, stores the exit code, and prints a new prompt. </br>  

For a builtin command like **cd**, the **Shell (bash)** takes a different approach. **Bash** does not make a **fork** and rest of the related tasks, instead **Bash** checks its **internal** table before checking the **PATH** variable whether the command **cd** is present. When **bash** that finds **cd** is **builtin** the following happens:
  1. **Bash** makes one **system call** to check if the directory we want to change to.  
  2. If the directory exists, permissions are checked, and if everything is in order, the current working directory is switched.  
  3. If the directory does NOT exist, an error message is printed to stdout.  

The following (generated) image describes the difference: </br>  
<img width="734" height="291" alt="image" src="https://github.com/user-attachments/assets/866e7d4d-83db-4e99-a395-b75e7cb06844" /> </br>  

### This is how the **Shell (bash)** treats **builtin** commands.
