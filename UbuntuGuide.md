## Ubuntu Init
```shell
sudo apt-get update -y
sudo apt-get install -y wget curl telnet tar unzip vim git
sudo apt-get install -y ssh
service sshd restart
```
* incase you need a http_proxy
```shell
export http_proxy=http://x.x.x.x:xxxx
export https_proxy=$http_proxy

touch /etc/apt/apt.conf.d/https_conf
cat <<EOF > /etc/apt/apt.conf.d/https_conf 
Acquire::https {
        Verify-Peer "false";
        Verify-Host "false";
}
EOF
```

## Ubuntu Desktop 16.04 VNC Setup
```shell
sudo apt install xfce4 xfce4-goodies tightvncserver -y

vncpasswd
```
* configuration

```shell
root@jsu-vm:/etc/systemd/system# cat vncserver@.service
[Unit]
Description=Start TightVNC server at startup
After=syslog.target network.target

[Service]
Type=forking
User=jsu
PAMName=login
PIDFile=/home/jsu/.vnc/%H:%i.pid
ExecStartPre=-/usr/bin/vncserver -kill :%i > /dev/null 2>&1
ExecStart=/usr/bin/vncserver -depth 24 -geometry 1600x950 :%i
ExecStop=/usr/bin/vncserver -kill :%i

[Install]
WantedBy=multi-user.target
```

```shell
jsu@jsu-vm:~$ cat ~/.vnc/xstartup
#!/bin/sh

xrdb $HOME/.Xresources
xsetroot -solid grey
#x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
#x-window-manager &

# Fix to make GNOME work
#export XKL_XMODMAP_DISABLE=1
#/etc/X11/Xsession

# Fix to make xfce work:
startxfce4 &
```
