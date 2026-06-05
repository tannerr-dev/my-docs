# Linux Commands

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

# Setting up a VPS
---
1. [connect SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
[cbp-vps](cbp%20vps)
```
ssh-keygen
```

2. update
```
sudo apt update
sudo apt upgrade
ls /var/run/reboot-required
reboot

# REAPEAT THESE STEPS AFTER REBOOT
```


3. lock down vps
```
# check for logins over ssh
sudo tail -n 10 -f /var/log/auth.log

# check user, if 0 you are root
id

# disable password login

- 
```

#### username
```
# change password of current user, (root)
passwd

# create new user
adduser <name>

#add user to sudo group
usermod -aG sudo <name>

#check if use group worked
groups <name>
```



```
#create ssh key for new user, on extenal device
ssh-keygen

#add public key from laptop into authorized keys directory 
~/.ssh/authorized_keys

# disable password login
## edit following files, find PassworAuthenication setting
/etc/ssh/ssh_config
/etc/ssh/ssh_config.d/
##cloud init?

sudo service ssh restart

# disable root login
#remove '#' comment in sshd_config
PermitRootLogin no

# network and firewall policy
# uncomplicated firewall (ufw)
# 22 for root, 80 http, 443 https?

sudo ufw allow 22    # Allow SSH
sudo ufw allow 80    # Allow HTTP
sudo ufw allow 443   # Allow HTTPS
sudo ufw status verbose
sudo ufw enable


# optional change ssh port to something else than 22 (for more security)
# you can lock down ports to specific ip addresses too

```

4. fail2ban
	- blocks IP at firewall level if there are multiple failed attmepts


5. automatic upgrades
```
sudo apt install unattended-upgrades
sudo dpkg-reconfigure unattended-upgrades

# check to see if it is running
sudo systemctl status unattended-upgrades
```
- a wizard should pop up, [docs link](https://github.com/mvo5/unattended-upgrades?tab=readme-ov-file#supported-options-reference)

5. [caddy](caddy.md)
	[docker-csshddy-ufw](docker-caddy-ufw.md)
```
# the caddy docs assume you are using it as a command line, we will be installing caddy as a service
# install the systemd service

sudo service caddy status

# update caddy file with domain name
/etc/caddy/Caddyfile

sudo service caddy restart
sudo service caddy reload

/var/www/
# do not have the website folders editable by the server user group
	change write access only to one user, not any servers

# changing owser of a directory
sudo chown tannerr:tannerr ttannerr.xyz/

# create a system link to perform a multifile pattern
ln -s /etc/caddy/sites-available/http-redirects /etc/caddy/sites-enabled/http-redirects

147.182.240.197

# send files over ssh
# specify files to send space separated, user login for ssh colon filepath
scp [<filename> <filename> <filename> ... ] <user>@<ip-address-or-domanin>:/path/to/directory

# send files using rsync (only transfers files that have changed)
rsync -azP $(pwd)/ <user>@<server-doman>:path/to/folder

# hide files from caddy
# insdie site code block
	file_server {
		hide .git
	}

# handle error
# insdie site code block
	handle_errors {
		respond "{err.status_code} {err.status_text}"
	}

there MUST be a space after the URL or IP before the {} in Caddyfile

# reverse proxy 
# insdie site code block
	reverse_proxy :3000

# servers in ~/hosts directory

# import configs from a folder
import conf.d/*.Caddyfile

## disable the config, add a '.disabled' on the end of the file name


```
symlink the readme into the content
```bash
ln -s $(pwd)/README.md $(pwd)/content/README.md
```

```
# github can create ssh deploy keys for cloning repos
# create ssh key on server, create key for specific repo not your whole github account

# install node under regular user account not root so if the server is compromised they can have access to everything

```

```
#manage long running processes with pm2 (or systemd)
# pm2 works well with node apps
```

6. [Python](Python.md)
```
# virtual environment
python3 -m venv env

source env/bin/activate
deactivate

# save the packeages of a project into a file to share on github 
pip freeze > requirements.txt

# install packes from file
pip install -r rquirements.txt


```
6. [go](go.md)
```
air
```

```

7. [docker](dev/dir/docker.md)
```
# add user to docker group to run commands without sudo
sudo usermod -a -G docker <user>

# you can build or compose on the production server but for larger apps you have a bulid server because it takes up a lot of compute resources

# docker compose addition
	restart: always

# run in detached mode
docker compose up -d

# list services?
docker ps



```

## syntax self host 101 notes

openvpn
wiregaurd
https://en.wikipedia.org/wiki/Software_load_testing

process manager or systemd to restart web server if it crashes
- use systemd to write a process manager for webservers to be hosted a vps or homelab
```
pm2
```

scp can transer files between your vps and laptop

ssh_config
- can be configured to specify username and port so you don't have to say it everytime you ssh
- you can specify a new ssh port in the config file
	- you can set up to not need to specify the user name too

- store ssh keys on yubikey and/or set up ssh keys on another machine? print it off
	- PAM modules?
- you can also set up 2fa?



we set up a new user and added that one to a group with sudo capabilities??
	then we set up the ssh to the new user

Issues with DNS resolution 
	Cloudflare TLS setting to FULL!!!
	
### Networking notes
```bash
dig
netcat
```


```
# after installing docker, add tannerr to the docker group
sudo usermod -a -G docker tannerr
```

opencode
add editor env
```bash
export EDITOR="nvim"
```

go, air, opencode
```bash
# golang
export PATH=/usr/local/go/bin:$PATH
export PATH=/home/tannerr/go/bin:$PATH

# opencode
export PATH=/home/tannerr/.opencode/bin:$PATH
export EDITOR="nvim"
```

alias's
```bash

alias gb='bash /home/tannerr/bash-scripts/gb.sh'

alias la='ls -a'
alias clsa='bash $HOME/bashh/clsa.sh'
alias src='bash $HOME/bashh/src.sh'
alias wttr='curl https://wttr.in/Minneapolis'

alias src='source /home/tannerr/.bashrc'

alias rrestart='docker build . -t tannerrrr/data-app-image && docker push tannerrrr/data-app-image:latest'

```


---


[Cron](cron.md)
```bash
cat /etc/crontab
which cron
service cron status
service cron start

crontab -l ##list
crontab -e ##edit

```

```bash
* * * * * echo hello >> /home/tannerr/hello.txt
# * * * * * /usr/bin/python3 /home/tannerr/data/programs/integration/reports/sales_scorecard.py >> /home/tannerr/cron.log 2>&1
#0 8 * * 1 /usr/bin/python3 /home/tannerr/data/programs/integration/reports/sales_scorecard.py >> /home/tannerr/cron.log 2>&1

```

```
# * * * * * echo hello >> /home/tannerr/hello.txt
# * * * * * /usr/bin/python3 /home/tannerr/data/integration/reports/sales_scorecard.py >> /home/tannerr/cron.log 2>&1
#0 8 * * 1 /usr/bin/python3 /home/tannerr/data/integration/reports/sales_scorecard.py >> /home/tannerr/cron.log 2>&1
0 6 * * 1 /usr/bin/python3 /home/tannerr/data/integration/reports/item_snapshot.py >> /home/tannerr/cron.log 2>&1
0 7 * * 1 /usr/bin/python3 /home/tannerr/data/integration/reports/contact_snapshot.py >> /home/tannerr/cron.log 2>&1

```


## SERVER DOCKER COMMANDS
### data-app

Local:
```
docker build . -t tannerrrr/data-app-image
```

```
docker push tannerrrr/data-app-image:latest
```

VPS:
```
docker pull tannerrrr/data-app-image
```

```
docker stop data-app && docker rm data-app && docker ps
```

```
docker run -d --name data-app -p 8080:8080 tannerrrr/data-app-image:latest
```


local all two:
```
sudo docker build . -t tannerrrr/data-app-image && sudo docker push tannerrrr/data-app-image:latest
```
vps all three:
```
docker pull tannerrrr/data-app-image && docker stop data-app && docker rm data-app && docker ps && docker run -d --name data-app -p 8080:8080 tannerrrr/data-app-image:latest
```


### data-connect

```
docker build --no-cache -t data-connect .
```

```
docker pull tannerrrr/data-connect:latest
```

```
docker run -d --rm --mount type=volume,src=integration-data,target=/integration/data --name data-connect -e NS_ID="treyhons@chromebookpars.com" -e NS_PW="" tannerrrr/data-connect:latest

```

### adding website to /var/www
1. create new dir
```bash
mkdir staticSite
```
2. change permissions
```bash
chmod +rw staticSite
```
3. deploy from dev machine
```bash
scp -r /home/tannerr/pockist/* user@7.77.77.777:/var/www/pockist/
```
4. configure caddy
```
pockist.com {
        root * /var/www/pockist
        file_server
        header {
                Cache-Control max-age=3600
        }
}
```
5. reload caddy config
```bash
sudo service caddy reload
```

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



