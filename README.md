# nut-config
Network UPS Tool (NUT) Advanced Configs: This is more for myself to easily config/use this tool to better manage my homelab. 
This is inspired by: [This Post](https://alioth-lists.debian.net/pipermail/nut-upsuser/2013-August/008557.html
) which helped the person created [This script](https://srackham.wordpress.com/2013/02/27/configuring-nut-for-the-eaton-3s-ups-on-ubuntu-linux/)

# Steps

### Install nut

In debian/Ubuntu nut is a part of the official repo so this is pretty straightforward:

```
sudo apt update
```

```
sudo apt install nut
```

### Setup `/etc/nut/nut.conf`

Change to the mode you need:

```
MODE=netclient
```


### Download the notify script

`wget https://raw.githubusercontent.com/yangjeep/nut-config/main/notifycmd`
 
 Then throw it into `/etc/nut` (ideally)

### Make changes in `upsmon.conf`

In `/etc/nut/upsmon.conf`, make sure you have the following lines configured:

```
MONITOR su700@server.example.com 1 upsmon secretpass slave

NOTIFYCMD "/etc/nut/notifycmd"

NOTIFYFLAG ONBATT SYSLOG+WALL+EXEC
NOTIFYFLAG ONLINE SYSLOG+WALL+EXEC
```

### Start nut-client services

```
systemctl enable nut-client
systemctl start nut-client
systemctl status nut-client
```

# References
[NUT Config examples at https://rogerprice.org/NUT/](http://rogerprice.org/NUT/ConfigExamples.A5.pdf)
