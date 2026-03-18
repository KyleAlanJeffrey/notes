from: https://systemd.io/
"*systemd is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as PID 1 and starts the rest of the system.

systemd provides aggressive parallelization capabilities, uses socket and D-Bus activation for starting services, offers on-demand starting of daemons, keeps track of processes using Linux control groups, maintains mount and automount points, and implements an elaborate transactional dependency-based service control logic. systemd supports SysV and LSB init scripts and works as a replacement for sysvinit.

Other parts include a logging daemon, utilities to control basic system configuration like the hostname, date, locale, maintain a list of logged-in users and running containers and virtual machines, system accounts, runtime directories and settings, and daemons to manage simple network configuration, network time synchronization, log forwarding, and name resolution.*"

### Commands

Edit service file
```
sudo systemctl edit --full cultivator-vision.service
```
View service file
```
sudo systemctl cat disk-monitor
```

## Making a Service File
NGINX Example Service file
```
# Stop dance for nginx
# =======================
#
# ExecStop sends SIGSTOP (graceful stop) to the nginx process.
# If, after 5s (--retry QUIT/5) nginx is still running, systemd takes control
# and sends SIGTERM (fast shutdown) to the main process.
# After another 5s (TimeoutStopSec=5), and if nginx is alive, systemd sends
# SIGKILL to all the remaining processes in the process group (KillMode=mixed).
#
# nginx signals reference doc:
# http://nginx.org/en/docs/control.html
#
[Unit]
Description=A high performance web server and a reverse proxy server
Documentation=man:nginx(8)
After=network.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t -q -g 'daemon on; master_process on;'
ExecStart=/usr/sbin/nginx -g 'daemon on; master_process on;'
ExecReload=/usr/sbin/nginx -g 'daemon on; master_process on;' -s reload
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid
TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

### **Attributes**

**WantedBy=multi-user.target**
"run this service on bootup"
Mult-user.target is an autostartup service that brings up all os level things. When stating this service is wanted-by mult-user.target, you're essentially stating, "run this service on bootup"

**Type=forking**
"How to run the file"
types=[`simple`, `exec`, `forking`, `oneshot`, `dbus`, `notify`, `notify-reload`, or `idle`:](https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html#Options)



##  Logging
Uses journalctl

### journalctl
from: https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs
"*Some of the most compelling advantages of `systemd` are those involved with process and system logging. When using other tools, logs are usually dispersed throughout the system, handled by different daemons and processes, and can be fairly difficult to interpret when they span multiple applications.*"

#### Commands

Show logs errors from most recent boot
```
journalctl -b -p err
```
Show logs from most recent boot
```
journalctl -b
```
List all of the boots
```
journalctl --list-boots
```

You can use relative language to see logs. Like yesterday, today, tomorrow.
```
journalctl --since yesterday
```
```
journalctl --since 09:00 --until "1 hour ago"
```

View logs by service
```
journalctl -u nginx.service
```
#### Timezones for JournalCTL
```
timedatectl status
```

```
sudo timedatectl set-timezone zone
```

