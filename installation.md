# Archlinux installation 

1. Using archlinux installation script)"[Archfi](https://github.com/MatMoul/archfi)"
2. [Manually installation](#manually-installation)
3. Install base-devel Git 
4. [Install Xorg](#install-xorg) 
5. Install Suckless DWM
6. [Wireless Network Setup](#wireless-network-setup)
7. [Install MPV with yt-dlp](#install-mpv-with-yt-dlp) 
---

### Archfi installation script 

`Curl -LO archfi.sf.net/archfi`

`sh archfi`

---

### Manually installation 

#### 1. Set the console keyboard layout

List available layouts

`ls /usr/share/kbd/keymaps/**/*.map.gz`

`loadkeys us.map.gz`  

#### 2. Verify the boot mode

`ls /sys/firmware/efi/efivars` 

if the command shows the directory without error, then the system is booted in UEFI mode.

#### 3. Network

#### 3.1 ip link

#### 3.2 iwctl

`iwctl` To get into interactive prompt

[iwd]# `help` list all available commands

[iwd]# `device list` list all Wi-Fi devices

[iwd]# `station *device* scan`  To scan for network

[iwd]# `station *device* get-networks` list all available network

[iwd]# `station *device* connect SSID` to connect to network

#### 4. Update System clock

`timedatectl set-ntp true` 

`timedatectl status` check the time status

#### 5. Partition the disk

#### 5.1 fdisk 

`fdisk -l` list attached drive

`lsblk` list device with mount point 

`fdisk /dev/the_disk_to_be_partitioned` modify partition tables

| fdisk command | function |
| :---: | :---: |
| m | manual |
| g | create a new GPT partition table |
| n | add a new partition |
| t | change a partition type |

Example layouts

| Mount point | Partition type | Suggested size |
| :---: | :---: | :---: |
| /mnt/boot or /mnt/efi | EFI system partition | At least 260MiB |
| [SWAP] | Linux swap | Square root to total memory |
| /mnt | Linux filesystem | Remainder of the device |

#### 5.2 Format partition 

`mkfs.fat -F 32 /dev/*efi_system_partition`

`mkswap /dev/swap_partition` 

`mkfs.btrfs /dev/root_partition`

#### 5.3 Creating Subvolumes and Mounting

```
mount /dev/*root_partition* /mnt

btrfs su cr /mnt/@
btrfs su cr /mnt/@home
btrfs su cr /mnt/@var
btrfs su cr /mnt/@tmp
btrfs su cr /mnt/@snapshots

umount /mnt

```
Mounting 

```
mount -o noatime,compress=lzo,space_cache=v2,subvol=@ /dev/*root_partition* /mnt
mkdir -p /mnt/{boot/efi,home,var,tmp,.snapshots}

```
Home 

`mount -o noatime,compress=lzo,space_cache=v2,subvol=@home /dev/sda3 /mnt/home`

var

`mount -o subvol=@var /dev/sda3 /mnt/var`




### Install base-devel and Git 
`sudo pacman -S base-devel git vim`



---

### To list enabled services

```
systemctl list-unit-files --state=enabled
```

---
### Install Xorg


`sudo pacman -S xorg-server xorg-xinit xorg-xrandr xorg-xsetroot`


##### copying xintic file to the user directory

`cp /etc/X11/xinit/xinitc ~/.xinitrc`

---
### Intall Suckless DWM

#### Install library for making DWM

`sudo pacman -S libx11 libxinerama libxft webkit2gtk`

#### Clone down Suckless DWM

Make a directory for the suckless DWM and get into it.

`git clone https://git.suckless.org/dwm`

`sudo make clean install`

#### Clone down Suckless ST and Dmenu as well

`git clone https://git.suckless.org/st`

`git clone https://git.suckless.org/dmenu`

---
### Getting Hardware Information 
#### To show all hardware infotmations
```
lshw 
```
#### To show CPU informations
```
lshw -C cpu
```
#### To show network hardware informations
```
lshw -C network
```
---

### Command "Dmidecode" - System informations based on SMBIOS
```
sudo dmideocde
```
#### To show memory size with dmidecode and grep
```
sudo dmidecode -t memory | grep -i size
```
---
### Command "lspci"
#### Using lspci with grep -i (ignore-case)
```
lspci | grep -i wireless
```
---
### To show Disk information
```
lshw -C disk -short
```
```
lsblk
```
```
fdisk -l 
```
---
### Wireless Network Setup
#### To show network connects
```
ip link
```
```
iw list
```


#### Setup wireless network with interface
```
nmtui
```
---
#### Setup wireless network with command "wpa_suppplicant"
#### Create wpa_supplicant config file
##### 1. Get the logical name of wireless network device

```
lshw -C network
```
#####    or 	

```
ip link
```

##### 2. Create /etc/wpa_supplicant/wpa_supplicant-$logicalnameofwihi.conf
```
touch /etc/wpa_supplicant/wpa_supplicant-wlp3s0.conf
```
#### 3. Adding the following line into the .conf file
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

---


### Install MPV with yt-dlp

#### To using MPV for playing youtube without slow buffering, youtube-dl has to be replace with yt-dlp.

```
https://github.com/yt-dlp/yt-dlp
```
##### or using yay to install yt-dlp for archlinux 
```
yay -S yt-dlp

```
#### Then edit mpv.conf, adding the following line.

```
script-opts=ytdl_hook-ytdl_path=${PATH-TO-YT-DLP}

```
##### or install yt-dlp-drop-in for Archlinux


#### Reference website
```
https://www.funkyspacemonkey.com/replace-youtube-dl-with-yt-dlp-how-to-make-mpv-work-with-yt-dlp
```



