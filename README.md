# BenGalles.github.io

## Download iso from archlinux mirror
* I chose a usa mirror and downloaded it, then checked the hash value to check the integrity of the file.

## Booting Environment
- In BIOS I chose the first option and pressed enter to load
- Used command `ip link` to connect to wifi and used `ping archlinux.org` to test
- Used `timedatectl status` to check the clock on the vm which returned the correct date, but the clock was 5 hours ahead so i used `timedatectl set-timezone America/Chicago` to change it
- To partition the drive i first used `fdisk -l` to see what I had already, then i used `fdisk /dev/sda` to create a partition from the current disk
- Then in the new window i used `n /dev/efi_systems_partition`, followed by primary partition `p` and partition `1` and I designated the first sector from `2048` to `634880` for a 309MiB partition, then i used `t /dev/efi_systems_partition` and `ef` to create an EFI partition type. Then for the next partition i used `n /dev/swap_partition`, `p`, `2`, `636928`, `1800192` then `t /dev/swap_partition`, `82` for linux swap. Then for the last partition, `n /dev/root_partition`, `p`, `3`, `1802240`, `41943039` for the rest of the disk and `t /dev/root_partition`, and `83` for main linux.
- Used `mkfs.ext4 /dev/sda3` to format main file, `mkfs.fat -F 32 /dev/sda1` to format the boot drive and `mkswap /dev/sda2` to make the swap file system
- Used `mount /dev/sda1 /mnt` and `swapon /dev/sda2` to start drives
