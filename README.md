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
# Set up locale
```
  vim /etc/locale.gen
```
### Once you have accessed the file, scroll and uncomment your preferred locale. In this case, we have decided to go with en_US.UTF-8 UTF-8
```
  locale-gen
  vim /etc/locale.conf
```
# Set up hostname
```
  vim /etc/hostname
```
### Write and save
  >murat(your hostname)

```
  vim /etc/hosts
```

### Write and save
  >127.0.0.1&nbsp;&nbsp;localhost
  >
  >::1                localhost 
  >
  >127.0.1.1          murat(yout hostname).localdomain         murat(yout hostname)

# Install netctl Network Manager
```
  pacman -Sy netctl
  pacman -Sy dhcpcd wpa-supplicant ifplugd
```
# Create a regular user
```
  passwd
  useradd -m murat(your username)
  passwd murat(your username)
  usermod -aG wheel,audio,video,optical,storage murat(your username)
```
# Set up sudo
```
  pacman -S sudo
  EDITOR=vim visudo
```
# Install GRUB bootloader
```
  pacman -S grub efibootmgr
  pacman -S os-prober
  grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
  grub-mkconfig -o /boot/grub/grub.cfg
  exit
  reboot
```
# Post Installation tasks
```
  ip link
```
  >The output confirms that our network interface is "enp0s3"

```
  su
  cp /etc/netctl/examples/ethernet-dhcp  /etc/netctl/custom-dhcp-profile
  cd /etc/netctl
  vim custom-dhcp-profile
```
**Changes from**
![Adsız](https://user-images.githubusercontent.com/51914434/135350696-a2e57d3b-86aa-4f5b-8699-0a10654ca67f.png)
**to**
![Adsız](https://user-images.githubusercontent.com/51914434/135351022-2647f9c6-dc96-418c-8506-3869e0ad0700.png)

