## Download iso from archlinux mirror
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
- To check partitions and create new partitions from the current disk i used:
```
fdisk -l
fdisk /dev/sda
```
- To create the first partition for boot, in the new window, I used:
```
n /dev/efi_systems_partition
p
1
2048
634880
t /dev/efi_systems_partition
ef
```
- Then for the swap partition, I used:
```
n /dev/swap_partition
p
2
636928
1800192
t /dev/swap_partition
82
```
- And for the last partition I used:
```
n /dev/root_partition
p
3
1802240
41943039
t /dev/root_partition
83
```
- In order to format and start/mount all the drives I used:
```
mkfs.fat -F 32 /dev/sda1
mkswap /dev/sda2
mkfs.ext4 /dev/sda3

mount /dev/sda1 /mnt
swapon /dev/sda2
```
