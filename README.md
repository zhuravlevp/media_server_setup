# Mini media server based on VLC or Kodi
## Settings
I'm using minimal server install (Debian, CentOS, Fedora)
### Debian 11
#### Install packages:
```
## For X server
sudo apt install -y xinit i3
## For scripts
sudo apt install -y git curl wget netcat unclutter
## VLC
sudo apt install -y vlc
```

#### Setting autologin:
add /etc/systemd/system/getty@tty1.service.d/autologin.conf
```
[Service]
ExecStart=
ExecStart=-/sbin/agetty -o '-p -f -- \\u' --noclear --autologin USERNAME %I $TERM
```

#### Start X:
add /home/USERNAME/.profile
```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 && ! -f /tmp/Xlock ]] && touch /tmp/Xlock && exec startx
export I3SOCK=$(DISPLAY=:0 i3 --get-socketpath) # for ssh command i3
```

#### Settng i3
add to /home/USERNAME/.config/i3/config
```
set $HOME /home/USERNAME

# Assign Workspaces:
for_window [class="vlc"] move to workspace $ws1
for_window [class="Kodi"] move to workspace $ws2

# Disable cursor
exec unclutter -root -idle 0 &

# Run apps
bindsym $mod+Shift+h exec $HOME/scripts/cursor.sh
bindsym $mod+Shift+p exec $HOME/scripts/past.sh
exec "[ -f /home/USERNAME/scripts/suspend.sh.lock ] && sleep 2 && echo USER_PASS | sudo -S /home/USERNAME/scripts/poweroff.sh"
exec kodi
exec i3-msg workspace $ws2

# Key Mod
exec xmodmap -e "keycode 121 = F8"
exec xmodmap -e "keycode 123 = equal"
exec xmodmap -e "keycode 122 = minus"
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
Section "Extensions"
    Option      "DPMS" "Disable"
EndSection

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
