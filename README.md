# HelpNvOptimus
**This repository or you can so say the article is created for clear installation of nvidia drivers for those laptops with optimus cards that hang intentionally.**

For example: you want to switch to linux, but you have a laptop on optimus card and so when you start in livecd (debinst, yast inst does not concern) hangs intentionally in video drivers nouveau or even with proprtar drivers. And you do not understand what to do.

There is a utility from nvidia called `bumblebee`for the video cards themselves, but it is long unsupported but still used. But it will have the same problem.

There are many utilities to customize optimus such as:
* [optimus-manager](https://github.com/askannz/optimus-manager) - utility for Arch linux
* [Envycontrol](https://github.com/bayasdev/envycontrol) - script from bayasdev, which edits configs. And adding xrandr commands from session managers.
* nvidia-prime - Utility from ubuntu, also changes the configs

Now I will also tell you how to install the distribution itself, this article will only cover Arch based, Ubuntu based/Debian based, OpenSUSE. 

for starters, if the distribution has debinst, yast inst, arch minimal and those with nouveau and other drivers disabled by default, then this option should not be used. For the rest:
- ***In grub boot loader select the desired boot and press e, where it says quet or splash write nomodeset (it disables video card drivers and starts in safe mode).***
- ***after that press ctrl + x***
- ***and now the system is loaded and we can install, but there is a problem with the screen resolution which cannot be changed.***
- ***as usual install the system via calamares or whatever and reboot.***
- ***then we see grub and boot again the same way.***
I forgot to mention that if grub has a safe mode option, it is better to boot from it.

### After we have installed the system we have to install the nvidia video drivers. We can download the dkms drivers from the off site or from the package manager.
### Arch linux based
- su
- pacman -Syyu
- pacman -S nvidia nvidia-utils nvidia-settings lib32-nvidia-utils vulkan-icd-loader

## OpenSUSE
### Adding repo
Tumbleweed: zypper addrepo --refresh https://download.nvidia.com/opensuse/tumbleweed NVIDIA
Leap: zypper addrepo --refresh 'https://download.nvidia.com/opensuse/leap/$releasever' NVIDIA
further
- su
- zypper upgrade
- zypper install x11-video-nvidia

## Ubuntu/Debian based
### Adding repo FOR DEBIAN(NO UBUNTU)
* add contrib non-free non-free-firmware in /etc/apt/sources.list
- su
- apt update
- apt dist-upgrade
- apt install nvidia-driver firmware-misc-nonfree

## any distr
### Download last drivers nvidia for nvidia.com

# As we have installed the driver on nvidia then do not reboot immediately, put optimus managers:
## optimus-manager(Arch linux)
### Installing yay(in case he doesn't exist in the system)
- git clone https://aur.archlinux.org/yay.git
- cd yay
- makepkg -si
- cd ..
- rm -rf yay #(if you don't need it already)
### Installing optimus-manager
- yay -S optimus-manager
***Now go to the config in /usr/share/optimus-manager.conf and change the lines:***
- startup_mode=integrated
- startup_auto_battery_mode=integrated
- startup_auto_extpower_mode=nvidia
- startup_auto_nvdisplay_off_mode=integrated
- startup_auto_nvdisplay_on_mode=nvidia
***available options are nvidia, hybrid, intel, integrated. If everything hangs intentionally, then nvidia, if not, then hybrid is fine.***
***then reboot and everything works, if there is a problem again, then in grub boot again with nomodeset and change***

# Envycontrol(any distr)
***Debian/Ubuntu there's a package, here's the latest release, [CLATS](https://github.com/bayasdev/envycontrol/releases/tag/v3.4.0).***
afterward: 
* su
* dpkg install envycontrol.deb
           
***Arch linux***
* yay -S envycontrol

***others***
* git clone https://github.com/bayasdev/envycontrol
* cd envycontrol

### Now showing you how to switch through it:
***Hybrid***
* su
* envycontrol -s hybrid --rtd3 #(1, 2, 3. detailed [CLICK](https://github.com/bayasdev/envycontrol)
* reboot
*** Nvidia ***
* su
* envycontrol -s nvidia --dm #(any dm(gdm,lightdm, sddm)) --coolbits #(detailed [CLICK](https://github.com/bayasdev/envycontrol)) --verbose --force-comp #(PRIME Synchronization)
* reboot
***integrated/intel***
* envycontrol -s integrated/intel
# Now you're all set, you can use it. And some more questions.
