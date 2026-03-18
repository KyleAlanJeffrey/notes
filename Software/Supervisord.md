Context: http://supervisord.org/introduction.html

**FROM THE WEBSITE**
*Supervisor is a client/server system that allows its users to control a number of processes on UNIX-like operating systems. It was inspired by the following:*

*Convenience

> It is often inconvenient to need to write `rc.d` scripts for every single process instance. `rc.d` scripts are a great lowest-common-denominator form of process initialization/autostart/management, but they can be painful to write and maintain. Additionally, `rc.d` scripts cannot automatically restart a crashed process and many programs do not restart themselves properly on a crash. Supervisord starts processes as its subprocesses, and can be configured to automatically restart them on a crash. It can also automatically be configured to start processes on its own invocation.

Accuracy

> It’s often difficult to get accurate up/down status on processes on UNIX. Pidfiles often lie. Supervisord starts processes as subprocesses, so it always knows the true up/down status of its children and can be queried conveniently for this data.

Delegation

> Users who need to control process state often need only to do that. They don’t want or need full-blown shell access to the machine on which the processes are running. Processes which listen on “low” TCP ports often need to be started and restarted as the root user (a UNIX misfeature). It’s usually the case that it’s perfectly fine to allow “normal” people to stop or restart such a process, but providing them with shell access is often impractical, and providing them with root access or sudo access is often impossible. It’s also (rightly) difficult to explain to them why this problem exists. If supervisord is started as root, it is possible to allow “normal” users to control such processes without needing to explain the intricacies of the problem to them. Supervisorctl allows a very limited form of access to the machine, essentially allowing users to see process status and control supervisord-controlled subprocesses by emitting “stop”, “start”, and “restart” commands from a simple shell or web UI.

Process Groups

> Processes often need to be started and stopped in groups, sometimes even in a “priority order”. It’s often difficult to explain to people how to do this. Supervisor allows you to assign priorities to processes, and allows user to emit commands via the supervisorctl client like “start all”, and “restart all”, which starts them in the preassigned priority order. Additionally, processes can be grouped into “process groups” and a set of logically related processes can be stopped and started as a unit.
"

## Commands and Services
**Supervisord**

Supervisord is the server component of supervisor. It starts, monitors, restarts child programs, handles logging and events. It uses a "Windows-INI" style configuration file usually located at `/etc/supervisord.conf`, containing sensitive data like unencrypted usernames and passwords.

**Supervisorctl**

Supervisorctl is the command-line client for supervisord, offering a shell-like interface to control and monitor subprocesses. It connects to supervisord via UNIX or TCP sockets and may require authentication. It usually shares the server's configuration file, but any file with a `[supervisorctl]` section is compatible.

**Web Server**

Supervisord offers a web interface with features similar to supervisorctl. It's accessible through a browser at `http://localhost:9001/` or a configured URL by enabling the `[inet_http_server]` section in the configuration file.