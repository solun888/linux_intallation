# Archlinux installation 

1. Using archlinux installation script)"[Archfi](https://github.com/MatMoul/archfi)"
1. Install base-devel Git 
1. [Install Xorg](#install-xorg) 
1. Install Suckless DWM

---

### Archfi installation script 

`Curl -LO archfi.sf.net/archfi`

`sh archfi`



---

### Install base-devel and Git 
`sudo pacman -S base-devel git vim`



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


 



