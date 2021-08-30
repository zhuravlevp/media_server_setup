# Mini media server based on VLC
## Settings
I'm using minimal server install (Debian, CentOS, Fedora)
### Debian 11
#### Install packages:
```
## For X server
sudo apt install -y xinit i3
## For scripts
sudo apt install -y git curl wget netcat
## VLC
sudo apt install -y vlc
```
#### Setting display:
##### Intel HD
add /etc/X11/xorg.conf.d/20-intel.conf
```
# Fix Tearing
# https://wiki.archlinux.org/title/intel_graphics#Tearing
Section "Device"
  Identifier "Intel Graphics"
  Driver "intel"
  Option "TearFree" "true"
EndSection

# Disable power management
# https://wiki.archlinux.org/title/Display_Power_Management_Signaling
Section "ServerFlags"
    Option "StandbyTime" "0"
    Option "SuspendTime" "0"
    Option "OffTime" "0"
    Option "BlankTime" "0"
EndSection
```
### Fedora 34
```
...
```
