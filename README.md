# Description
Install VNC server called x11vnc in Ubuntu. Tested in Ubuntu 20.04 and Ubuntu 24.04

## Install VNC Server
```
$ sudo apt install x11vnc
```

## Configure vnc authentication access
Execute this command to set default vnc password for simur account
```
$ x11vnc -storepasswd
```

## Create service daemon
Create x11vnc service called **x11vnc.service**

```
$ sudo nano /lib/systemd/system/x11vnc.service
```

If you have some problems at service starting point check the display Id from 1 to 0:

```
[Unit]
Description=x11vnc server for simur
After=graphical.target
Wants=graphical.target

[Service]
Type=simple
User=simur
ExecStart=/usr/bin/x11vnc -display :1 -auth /home/simur/.Xauthority -usepw -forever -shared -loop
Restart=on-failure

[Install]
WantedBy=graphical.target
```

In my Ubuntu 20.04 I have this execution start configuration

```
ExecStart=/usr/bin/x11vnc -display :1 -auth guess -passwd !Thingtrack2010 -forever
```

## Activate service and start
If don't want restart the server, execute this commands:

```
$ sudo systemctl daemon-reload
$ sudo systemctl enable x11vnc
$ sudo systemctl start x11vnc
```

## Limitar GNOME a un workspace
Sometimes maybe you have problems with the virtual screens in your server then execute these commands to deactivate these virtual servers

```
$ gsettings set org.gnome.mutter dynamic-workspaces false
$ gsettings set org.gnome.desktop.wm.preferences num-workspaces 1
```

## Install VNC client
Now download and install VNC Client like Real VNC Viewer from:

```
https://www.realvnc.com/en/connect/download/viewer/
```
