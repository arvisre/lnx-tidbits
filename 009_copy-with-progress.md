# Scenario: Copying large file from disk to usb flash drive </br>  
I was copying a 4.5GB iso file from my Fedora Workstation to a USB stick (using Nautilus). Surprisingly, the copy process completed in a jiffy.  
However, when I ejected the usb stick and tried to unplug it, I was notified that "**writing is still going on**".  
I was wondering whether Linux systems have a copy progress-bar feature such that similar situations can be avoided? </br>  

# What's actually happened: </br>  
It appears that when I copy a file in Linux systems, "the kernel writes to a page cache in RAM first and reports that the process is done". However, the actual "writing data to usb stick" takes place in the background and can take a few minutes". So this is the reason I could NOT eject and unplug the usb flash drive.

# How can I ensure that this situation does NOT happen again? </br>  
Since the GUI did NOT show me a **copy-progress-bar** (or) the copy-progress-bar was tiny in some corner that I missed noticing it, I need to use the command line to ensure that the copy process happens immediately. I do NOT want to assume that the copy is completed only to find out it wasn't while unplugging the external storage device. </br>  

