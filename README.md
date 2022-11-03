## Download ISO
* I chose a usa mirror and downloaded it, then checked the hash value to check the integrity of the file.

## Booting Environment
- In BIOS I chose the first option and pressed enter to load
- To link vm with wifi and check to see if wifi was working i used:
```
ip link
ping archlinux.org
```
- To check time and correct it since it was wrong i used:
```
timedatectl status
timedatectl set-timezone America/Chicago
```
- To check partitions and create new partitions (BIOS/GPT) from the current disk i used:
```
fdisk -l
fdisk /dev/sda
g
```
- To create the future boot drive I used:
```
n
-
-
+1M
t
4
```
- Then for the swap drive I used:
```
n
-
-
+1G
t
-
19
```
- and for the main drive I used:
```
n
-
-
-
t
-
23
w
```
- In order to format and start/mount all the drives I used:
```
mkswap /dev/sda2
mkfs.ext4 /dev/sda3

swapon /dev/sda2
mount /dev/sda3 /mnt
```
## Installation/Configuration
- For installing the archlinux packages I used:
```
pacstrap -K /mnt base linux linux-firmware
```
- To generate an Fstab file I used:
```
genfstab -U /mnt >> /mnt/etc/fstab
```
- Then to change root into the system I used:
```
arch-chroot /mnt
```
- To set the timezone of the system I used:
```
ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime
hwclock --systohc
```
- Installed vim using:
```
pacman -S vim
```
- I used vim to uncomment the line "en_US.UTF-8 UTF-8" using:
```
vim /etc/locale.gen
```
- Then to setup my locales, I used:
```
locale-gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```
- To change the root password I used:
```
passwd
root
root
```
### Boot Loader/Desktop Environment
- I first created a boot drive using:
```
pacman -S grub
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```
- To install gnome i used
```
pacman -S gnome
pacman -S gnome-tweaks
systemctl enable gdm
pacman -S networkmanager
```
- Then I rebooted the VM using:
```
exit
reboot
```
### Finishing up
- Once inside the DE I used:
```
systemctl start NetworkManager
```
- To install a new shell (zsh) used:
```
pacman -S zsh
```
- To create codi account:
```
useradd -m -U -G wheel -s /usr/bin/zsh codi
passwd codi
GraceHopper1906
GraceHopper1906
passwd -e codi
```
- To create my account:
```
useradd -m -U -G wheel ben
passwd ben
ben
ben
```
- To login to the class gateway I turned on my vm and used:
```
ssh sysadmin@10.10.1.113
```
- To add some aliases I used:
```
alias ..='cd ..'
alias printmycurrentdirectory='pwd'
alias la='ls -a'
```
- To add some fun colors to my terminal I used:
```
export PS1=`printf "\033[33m$ \033[44m \033[107m"`
```
