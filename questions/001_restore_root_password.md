# Restore root password

It can be preliminary task for starting Your exam. It is crucial to know this procedure by heart. 

###Question:
 You do not know the root password but You have physical access to the machine. Create new root password
and log into the system.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

###Answer:

* During boot time when GRUB loader screen is presented press *e* key. That will open an editor with current kernel boot options.
* Find the line starting with ***linux16***. At the end of that line add **rd.break** and press ***Ctrl-x*** to restart the 
system with new option.
* What this actually does is taking You to the target right at the end of the boot stage - before root filesystem is mounted (on /).
* Type ***mount -o remount,rw /sysroot***. This actually gets You RW access to the filesystem. ***/sysroot*** folder is Your 
normal ***/*** hierarchy.
* Type ***chroot /sysroot*** to make this folder new root directory.
* Now it is time to change the root password (that is what we are here for right?) - type ***passwd*** and provide new
password.
* In order to finish the task **SELinux** must be taken care of. If not, contents of ***/etc/shadow*** will be messed up. There are
two commands to be provided:
```
 load_policy -i 
 chcon -t shadow_t /etc/shadow
```

* Type ***exit*** twice (with pressing ENTER after each one)
* Now You can log into the system using new password