---
title: "VPS"
weight: 1
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
