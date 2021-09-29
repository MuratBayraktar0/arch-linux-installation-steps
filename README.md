# Begin the installation of Arch Linux
```
  ls /sys/firmware/efi/efivars
  ping google.com
```
# Update time and date
```
  timedatectl set-ntp true
  timedatectl status
```
# Create & format Linux partitions
```
  cfdisk
```
![Adsız](https://user-images.githubusercontent.com/51914434/135347668-ee7b3552-6d72-4072-85cf-029ce7239b05.png)

# Format and mount the partitions
```
  mkfs.ext4 /dev/sda5
  mkswap /dev/sda6
  swapon /dev/sda6
  mount /dev/sda5 /mnt
  mkdir /mnt/efi
  mount /dev/sda1 /mnt/efi
```
# Install base system and other required Linux firmware packages
```
  pacstrap /mnt base linux linux-firmware
```
# Generate fstab file
```
  genfstab -U /mnt >> /mnt/etc/fstab
```
# Setup timezone
```
  arch-chroot /mnt
  ln -sf /usr/share/zoneinfo/Europe/Istanbul /etc/localtime
  hwclock --systohc
  pacman -Sy vim
```
