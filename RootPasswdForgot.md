### CentOS 6 ###

- Click [View Console] to access the console and click the send CTRL+ALT+DEL button on the top right. Alternatively, you can also click [RESTART] to restart the server.
- You will see a GRUB boot prompt telling you to press any key - you have only a few seconds to press a key to stop the automated booting process. (If you miss this prompt you will need to restart the VM again)
- At the GRUB prompt, type "a" to append to the boot command.
- Add the text "single" and press enter.
- System will boot and you will see the root prompt. Type "passwd" to change the root-password and then reboot again.

### CentOS 7 ###

- Click [View Console] to access the console and click the send CTRL+ALT+DEL button on the top right. Alternatively, you can also click [RESTART] to restart the server.
- As soon as the boot process starts, press ESC to bring up the GRUB boot prompt. You may need to turn the system off from the control panel and then back on to reach the GRUB boot prompt.
- You will see a GRUB boot prompt - press "e" to edit the first boot option. (If you do not see the GRUB prompt, you may need to press any key to bring it up before the machine boots)
- Find the kernel line (starts with "linux16"), change ro to rw init=/sysroot/bin/sh.
- Press CTRL-X or F10 to boot single user mode.
- Access the system with the command: chroot /sysroot.
- Run passwd to change the root password.
- Reboot the system: reboot -f.

### Debian, Ubuntu ###

- Click [View Console] to access the console and click the send CTRL+ALT+DEL button on the top right. Alternatively, you can also click [RESTART] to restart the server.
- As soon as the boot process starts, press ESC to bring up the GRUB boot prompt. You may need to turn the system off from the control panel and then back on to reach the GRUB boot prompt.
- You will see a GRUB boot prompt - press "e" to edit the first boot option. (If you do not see the GRUB prompt, you may need to press any key to bring it up before the machine boots)
- Find the kernel line (starts with "linux /boot/") and add init="/bin/bash" at the end of the line (On CentOS 7, the line may start with linux16).
- Press CTRL-X or F10 to boot.
- System will boot and you will see the root prompt. Type "mount -rw -o remount /" and then "passwd" to change the root password and then reboot again.

### FreeBSD ###

- The boot menu has an option to boot into single-user mode. Press the key for single user mode (2). At the root prompt, type "passwd" to change the root password and then reboot again.

### CoreOS ###

CoreOS by default uses SSH key authentication. On Vultr, a root user and password are created. If an SSH key is selected when creating the VPS, this SSH key can be used to login as user "core".
It is possible to reset the standard root login by executing "sudo passwd" as user "core". Login as "core" using the SSH key first.
If you lost your SSH key, then you can login as the "core" user by editing the grub loader. Follow these steps:

- Click [View Console] to access the console and click the send CTRL+ALT+DEL button on the top right. Alternatively, you can also click [RESTART] to restart the server.
- You will see a GRUB boot prompt - press "e" to edit the first boot option. (If you do not see the GRUB prompt, you may need to press any key to bring it up before the machine boots)
- At the end of the line that begins with "linux$" add " coreos.autologin=tty1" (no quotes).
- Press CTRL-X or F10 to boot. You will be logged in as "core" when the system boots.
- Remember to reboot your server after you have reset your login.
