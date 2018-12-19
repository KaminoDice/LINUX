# step 1.
## download ubuntu-14.04-desktop-amd64.iso; 
## abstract file initrd.lz and file vmlinuz.efi from this .iso file in its casper directory, copy them;
## put the .iso file, initrd.lz, and vmlinuz.efi into C:/ (other root partion may cause a error)

# step 2.
## download EasyBCD, start it;
## "Add New Entry" >> "NeoGrub" in "Operating Systems" >> "Install" >> "Configure" (It may fail. If so, do "Add Entry" in "Portable/External Media", "Remove" in "NeoGrub", then "Install" again. This time, "Configure" may work.) MAKE SURE: Do Not insert a Portable/External Media operation (Add Entry) into this procedure!
## "Configure" will open a file named "menu.lst", append below commonds at the end of this file.  
title Install Ubuntu  14  
root (hd0,0)  
kernel (hd0,0)/vmlinuz.efi boot=casper iso-scan/filename=/ubuntu-14.04-desktop-amd64.iso ro quiet splash locale=zh_CN.UTF-8  
initrd (hd0,0)/initrd.lz  
TIPS: (a) 0 in (hd0,0) is the number of partation which you put the .iso file, initrd.lz, and vmlinuz.efi into. you can get this number by checking a software named "DiskGenius". In general, number of C: is 0, D: (4), E: (5), F: (6), if you name your partions in the order of C, D, E, F.  
(b) make sure the name of file vmlinuz.efi you abstract from .iso file must be in consisstent with "kernel (hd0,0)/vmlinuz.efi ...". otherwise, you will definitely get a error 15, which is "File not found".  
(c) If you want to install ubuntu system into the partation F:, then you can not put the .iso file, initrd.lz, and vmlinuz.efi in this partation F. otherwise, you will stuck in "Detecting file system".  
## check "Edit Boot Menu", if you see "NeoGrub Bootloader" in "Modify Menu Entries", restart you computer, use up and down to enter "NeoGrub Bootloader".  

# step 3.
## open a terminal, execute the command "sudo umount -l /isodevice".
## start to install ubuntu.
## swap 4GB ( the same as your computer main memory )
## /boot 256MB
## /home 30GB
## /     the left space
