---
title: "Desktop"
weight: 1
---
# Desktop Commands

For Ubuntu (debian) based systems.

## Everyday things

### Date and time
```bash
date
```

### Audio
#### Volume
```bash
alsamixer
```
#### Audio Drivers
WirePlumber Control, PipeWire session manager. (audio / video drivers)
```bash
wpctl status
```
### Screen Shot
Take a screenshot
```bash
import screenshot.png
```
### Night Shade
```bash
redshift -O 5000 # intensity 5000
redshift -O 3000 # lower the number the darker it gets
redshift -x # resets
```

## Display
List connected displays
```bash
xrandr
```
This shows all connected monitors and their current resolutions and refresh rates.

Set display resolution and position
```bash
xrandr --output HDMI-1 --mode 1920x1080 --rate 60

#mirror
xrandr --output HDMI-2 --same-as eDP-1 --mode 1920x1080
#extend
xrandr --output HDMI-2 --mode 1920x1080 --pos 0x0 --output eDP-1 --mode 1920x1080 --pos 1920x0

```
Search for connected display names
```bash
xrandr -q | grep " connected"
```

change brightness
```bash
xrandr --output <display name> --brightness 0.5

xrandr --output eDP-1 --brightness 0.5
```

## WIFI
**List available networks:**
```bash
nmcli device wifi list
```

**Connect to a network:**
```bash
nmcli device wifi connect "<SSID>" password "<PASSWORD>"
```

**Disconnect from a network:**
```bash
nmcli device disconnect wlan0
```

**Show connection status:**
```bash
nmcli connection show
nmcli device status
```

**Enable/disable WiFi:**
```bash
nmcli radio wifi on
nmcli radio wifi off
```

**Forget a saved network:**
```bash
nmcli connection delete "<SSID>"
```

A terminal-based interface that's easier than raw commands:

```bash
nmtui
```
## Bluetooth

Bloothooth was so annoying I made a [CLI/TUI wrapper called `bt`](https://github.com/tannerr-dev/bt-cli)

```bash
bluetoothctl power on
bluetoothctl power off

bluetoothctl scan on
bluetoothctl scan off

bluetoothctl pair <MAC_ADDRESS>

bluetoothctl connect <MAC_ADDRESS>
bluetoothctl disconnect <MAC_ADDRESS>

bluetoothctl devices
```

To create a connection with the built-in utils, you can follow this slightly more manual process using bluetoothctl.
to get the MAC address of your device

```bash
hcitool scan  
```

use bluetoothctl in interactive mode

```
bluetoothctl
power on  # in case the bluez controller power is off 
agent on
scan on  # wait for your device's address to show up here
scan off
trust MAC_ADDRESS
pair MAC_ADDRRESS
connect MAC_ADDRESS

sudo hcitool cc 94:23:6E:6F:23:9D

```



Device F8:73:DF:CF:A8:ED Beats Studio Pro

```
bluetoothctl
scan on

pair F8:73:DF:CF:A8:ED
trust F8:73:DF:CF:A8:ED
connect F8:73:DF:CF:A8:ED

bluetoothctl devices
bluetoothctl scan on

bluetoothctl pair F8:73:DF:CF:A8:ED
bluetoothctl trust F8:73:DF:CF:A8:ED
bluetoothctl connect F8:73:DF:CF:A8:ED
```

then quickly pair and connect with bluetoothctl

You can add keybindings to your `~/.config/i3/config` file for quick access:

```
bluetoothctl info F8:73:DF:CF:A8:ED

```

## Basic unix/cli programs

```bash
ps aux | head -n 1
```

```
cat /etc/issue
```

```
ls /var/run/reboot-required
```

open a tar file? or make one..
```
tar -xjf file.tar.gz2
```
waterfox?
```
mv waterfox ~/.local/opt/
~/.local/opt/waterfox/waterfox
```

```bash
fwupdmgr get-updates
fwupdmgr upgrade
fstrim -v --all

# check the hard disk space
df -h

grep -r "error" /var/log

scp -r /home/ttannerr/stuff/apps/tannerrdotcom/dist tannerr@7.77.77.777:/home/tannerr/
rsync -a ~/dir1 username@remote_host:destination_directory

sudo hostnamectl set-hostname host.example.com --static
which sh
pwd

whoami
passwd

chmod
chmod +rwx filename # – Adds read, write, and execute permissions.
chmod -rwx directoryname #– Removes all permissions.
chmod +x filename #– Grants executable permission.
chmod -wx filename #– Removes write and execute rights.

sudo chown tannerr:tannerr /opt/pockist/


# find and kill processes
ps aux | grep 
kill [PID]
kill -9 pid
who -u

find
cat
less

htop

# uncomplicated firewall
ufw

# dig into Dns records
dig
netcat

# change owner of folder
sudo chown tannerr:tannerr ttannerr.xyz/

# link, symbolic link, creates a folder pointer essentially 
ln -s

# file transfer to server
scp
rsync
github #obviously

# process manager
pm2 # not native, for node apps
# or
systemd # native to linux

```bash
sudo dpkg -i package_file.deb
```


```
# remove report error dialog?
sudo rm /var/crash/*

```



### json parser?
```
jq

```



systemctl stop postgresql



edit .bashrc 
	echo "hello from .bashrc"


disable double tap drag Ubuntu / pop*
bash command
```bash
gsettings set org.gnome.desktop.peripherals.touchpad tap-and-drag false
```

```bash
# disable and enable keyboard
xinput --list
xinput --disable 11
xinput --enable 11
```
```
export PATH=$PATH:/home/user/bin
cp -r supastro ~/web-dev/calc

# Remove "string_to_remove" from all filenames
rename 's/string_to_remove//' *

# re runs previous command but in sudo mode
sudo!! 

```

```bash
lsd --tree --depth 2 -I node_modules
```

```bash
alias my_script='bash /path/to/lsdd.sh'
source ~/.bashr
```

delete then watch a log file and print to console every 1s 
```bash
truncate -s 0 scraper.log && watch -n 1 "cat scraper.log | tail -n 20"
```


```
chmod +x myscript.sh
```

---


### Disable Brave scrollable tabs
```
brave://flags/#brave-change-active-tab-on-scroll-event
```
Change active tab on scroll event
Change the active tab when scroll events occur on tab strip. – Linux
#brave-change-active-tab-on-scroll-event




### tap to click START trackpad settings
#### NOTES
Check out the xinput command. 
```
xinput list 
```
will give you a list of input devices; 
find the ID of the one which looks like a touchpad. 
Then do 
```
xinput list-props <device id>
```
which should tell you what properties you can change for the input device. 
You should find one called something like Tapping Enabled and a number in 
parens after it (in my case, its libinput Tapping Enabled (276). Finally, 
run 
```
xinput set-prop <device id> <property id> 1
```
, and tapping should work.
#### COMMANDS
```
xinput list 
xinput list-props <device id>
xinput set-prop <device id> <property id> 1

# natural scrolling
xinput set-prop 9 317 1
xinput set-prop 10 317 1

# tap to click
xinput set-prop 9 322 1
xinput set-prop 10 322 1
xinput set-prop 13 322 1
xinput set-prop 13 346 1
xinput set-prop 13 346 1
```



### MOUSE SPEED
```
xinput list 
xinput list-props <device id>
xinput set-prop <device id> <property id> 1
```

the setting you are looking for is the Coordinate Transformation Matrix

You can use the default Value 1.000000, 0.000000, 0.000000, 0.000000, 1.000000, 0.000000, 0.000000, 0.000000, 1.000000

and change the last value. You can do it like this:

```
ctmVal=3
xinput set-prop 12 "Coordinate Transformation Matrix" 1, 0, 0, 0, 1, 0, 0, 0, $ctmVal
xinput set-prop 10 190 1, 0, 0, 0, 1, 0, 0, 0, 3
```
the higher $ctmVal in this case, the slower the mouse speed



THEME NONSENSE START
tried this but doesn't work
.config/gtk-3.0 or 4.0/settings.ini
[Settings]
gtk-application-prefer-dark-theme=true
sudo apt install lxappearance
sudo apt install adwaita-icon-theme gnome-themes-extra
gsettings set org.gnome.desktop.interface gtk-theme "Adwaita-dark"
non of this worked to change the default files/nautilus or calc 
or zed, the system theme was never changed
THEME NONSENSE END


#### theme that actually worked?
```
$HOME/.config/xdg-desktop-portal/portals.conf
```
with contents:
```
[preferred]
default=gtk;wlr
```




Trackpad scroll
Edit /usr/share/X11/xorg.conf.d/40-libinput.conf
Add there Option "NaturalScrolling" "True" like this:
Section "InputClass"
        Identifier "libinput touchpad catchall"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        Option "NaturalScrolling" "True"
EndSection
 Trackpad scroll END


---



