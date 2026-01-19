## Description
Install VNC server called x11vnc in Ubuntu. Tested in Ubuntu 20.04 and Ubuntu 24.04
# Install x11vnc
```
$ sudo apt install x11vnc
```

# set default vnc password for simur user
Execute this command
```
$ x11vnc -storepasswd
```

# Create service
Create x11vnc service called **x11vnc.service**

```
$ sudo nano /lib/systemd/system/x11vnc.service
```

If you have problems, check the display Id from 1 to 0:

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

# Reload services ans enable x11vnc and restart server
If don't want restart the server, execute this commands:
```
$ sudo systemctl daemon-reload
$ sudo systemctl enable x11vnc
$ sudo systemctl start x11vnc
```

# Limitar GNOME a un workspace
Sometimes maybe you have problems with the virtual screens in your server then execute these commands to deactivate these virtual servers

```
$ gsettings set org.gnome.mutter dynamic-workspaces false
$ gsettings set org.gnome.desktop.wm.preferences num-workspaces 1
```