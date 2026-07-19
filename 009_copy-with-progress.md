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
I am going to do the same process, but this time combining both the commands. Also I'm going to run the **date** command to find out how long it took.

