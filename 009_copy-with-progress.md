# Scenario: Copying large file from disk to usb flash drive </br>  
I was copying a 4.5GB iso file from my Fedora Workstation to a USB stick (using Nautilus). Surprisingly, the copy process completed in a jiffy.  
However, when I ejected the usb stick and tried to unplug it, I was notified that "**writing is still going on**".  
I was wondering whether Linux systems have a copy progress-bar feature such that similar situations can be avoided? </br>  

# What's actually happened: </br>  
It appears that when I copy a file in Linux systems, "the kernel writes to a page cache in RAM first and reports that the process is done". However, the actual "writing data to usb stick" takes place in the background and can take a few minutes". So this is the reason I could NOT eject and unplug the usb flash drive.

# How can I ensure that this situation does NOT happen again? </br>  
Since the GUI did NOT show me a **copy-progress-bar** (or) the copy-progress-bar was tiny in some corner that I missed noticing it, I need to use the command line to ensure that the copy process happens immediately. I do NOT want to assume that the copy is completed only to find out it wasn't while unplugging the external storage device. </br>  

# 1. Using the command "sync" </br>
The command **sync** can be used independently after issuing the command **cp** or in conjunction with the command **cp**. </br>  
I am going to copy an ISO file from **/home/as/Downloads** to an USB stick at **/run/media/as/AS128GxFAT/ISOs/**. </br>  
After executing the **cp** command, I executed the **sync** command. Then from the **dock** I tried to **Eject** the USB stick. This is when I encountered the notification as shown in image: </br>  
<img width="1274" height="316" alt="Screenshot From 2026-07-19 15-04-07" src="https://github.com/user-attachments/assets/0012e57e-97ef-43b9-9385-63080559fc42" /> </br>
I am going to do the same process, but this time I'm going to run the **date** command to find out how long it took. </br>  
<img width="1153" height="335" alt="Screenshot From 2026-07-19 16-11-30" src="https://github.com/user-attachments/assets/7e2bef73-8158-41c0-b81b-a0dec9cb3475" /> </br>  
It took almost two and a half minutes to complete the job. </br>  
**NOTE** - When the **sync** command is executed, the control does NOT return until the job finishes. Only when the sync completes do I see the prompt. </br>  
I am now going to combine the commands with the "**&&**" operator such that the second command/condition **sync** executes/is-true only when the first command/condition **cp** executes/is-true. </br>  
<img width="1216" height="172" alt="Screenshot From 2026-07-19 16-25-59" src="https://github.com/user-attachments/assets/aa9c50e4-4203-4de3-bd9f-5aa5e5061226" /> </br>  

#2. Using the command "rsync" </br>  
I can use the **rsync** command with the **--progress** option to display a progress-bar of the copy process. I also include the **-a** and **-h** options. The **-a** option packs a lot of options together to keep the **metadata** intact - such as copying recursively and preserving permissions, timesteps, owner and group details.
So I'm going to use the same ISO file from the same source path and copy to the same destination path with the **rsync** command.
