# Chrultrabook
 
## Introduction
This documents the process to convert an Acer C720 or C740 Chromebook into what is known as a "Chrultrabook" - an unlocked Chromebook flashed with custom firmware (UEFI BIOS ROM) to allow installation of a non-Google OS (Windows/Linux).
 
## Resources
Backups are included here, but using the latest versions is recommended.
 
### MrChromebox
MrChromebox is the author and maintainer of the automatic ROM flashing script that makes this process so accessible. The script is made to be run from inside of the stock ChromeOS terminal, after the OEM-unlocked Chrombook is booted in Developer mode to enable shell access.
https://docs.mrchromebox.tech
 
### Chrultrabook
Chrultrabook is the team that maintains the custom firmware. Google's firmware is forked from an upstream open source project, but patches, bugfixes, and configurations are backported to this independently, since Google rarely keeps its own public repositories up-to-date. Their community forum is very active and useful.
https://docs.chrultrabook.com
 
### WeirdTreeThing
WeirdTreeThing (find on GitHub) developed a popular and ubiquitous post-installation script to fix audio drivers for the sound cards on many Chromebooks. Intel pre-shipped their own installed patch that is lost in the upgrade which solves a major power delivery bug, causing speakers to pop and permanently break. This particular machine is not recognized by the script, and more investigation is needed into whether the machine is affected (e.g., check avs product number).
 
### ArchLinux Wiki
The Arch Linux wiki has an excellent page dedicated to the Acer C720 model chromebook (not to be confused with the C720P touchscreen model), as well as various post-installation tweaks useful for Chromebooks.
https://wiki.archlinux.org/title/Acer_C720_Chromebook
https://wiki.archlinux.org/title/Chrome_OS_devices
 
### Pop!_OS
Pop!_OS is a fork of Ubuntu marketed by System76 with a custom (newer) kernel that is compatible with the Chrultrabook firmware (or drivers, I forget the exact details). Out of the biggest 3 base distros (Arch, Fedora, Debian), only Arch and Fedora (and their derivatives) are officially supported, with Pop!_OS being the sole exception of a supported Debian-based distribution. This isn't ideal, but it is a straightforward choice; Arch requires lots of post-installation setup, and its simplified fork EndeavourOS's author is currently taking a break; Fedora still suffers from a few of the same bugs as Debian and requires lots of convenience tweaking out of the box (patented codecs, etc.), and the Ultramarine fork that solves this makes its own binding creative decisions; leaving Pop!_OS, though possibly no longer a priority for its developers at System76, as the most compatible, available, and similar to Ubuntu option, which is already familiar and a one-click install.
 
## Steps
The device was purchased second-hand from a bulk supplier after being recycled by a local school district. These steps may not be perfectly ideal, complete, or accurate, but should give a sense (from memory) of the procedure taken. 
 
1. Initially, the device was still seemingly managed by the school's enterprise account, and not properly decomissioned. However, this does not seem to have posed any issue after erasing the harddrive by enabling, then disabling, then re-enabling Developer Mode (ESC + REFRESH + POWER, then CTRL + D). Even if Developer Mode is blocked at first, the process will erase the harddrive and lead to the account setup screen. After logging in with another (personal) Google account, you become the new device owner and can now access Developer Mode.
 
2. With Developer Mode enabled, ignore warnings and boot. The Chrome OS setup screen should appear. Connect to Wi-Fi, but skip creating an account and simply browse as guest.
 
3. Open the Chrome browser and open the proprietary `crosh` terminal with CTRL+ALT+T, then run `shell` to enter the actual shell made available by Developer Mode.
 
4. Now that full access is confirmed, shut down the device, unscrew and remove the backplate, then remove the special "write-protection" screw on the motherboard (refer to diagrams, it is approximately between and above the battery and SSD). Replace the backplate, but don't screw it back in yet if the SSD will be changed.
 
5. Repeat steps 2 and 3, then run MrChromebox's Firmware Utility Script `cd; curl -LO mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh` and choose "Install/Update UEFI (Full ROM) Firmware", then reboot. You should boot into a BIOS.
 
6. Shut down the computer, remove the back panel again to install a higher-capacity replacement SSD, then screw everything back together.
 
7. Create a Pop!_OS bootable ISO USB with Rufus on another computer, and insert it into the Chromebook.
 
8. Turn on the computer, boot from USB, and proceed through the installer. Choose custom installation to open Gparted and erase and re-format the harddrive (for safety). Ensure that it's GPT and not MBR partitioned. Then back out, and use the default install method. Finally, allow it to reboot when prompted.
 
9. After rebooting into Pop!_OS, download and install software updates.
 
10. Re-map the top row keyboard keys to match the ChromeOS labels using `localectl set-x11-keymap us chromebook`.
 
11. Full power cycle the laptop, and enjoy!