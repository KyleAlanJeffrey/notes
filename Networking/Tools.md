## Wifi 

See devices on local network
```
arp -a
```

## Bluetoothctl
Very common bluetooth module for linux

Show the bluetooth module
```
bluetoothctl show
```
Power on 
```
bluetoothctl power on
```
Restart
```
sudo systemctl restart bluetooth
```

## Netcat
Great tool for sniffing [[UDP]]/[[TCP]] Ports

By default, netcat operates by initiating a TCP connection to a remote host.

The most basic syntax is:
```
netcat [options] host port
```

If you would like to send a UDP packet instead of initiating a TCP connection, you can use the `-u` option:

```
netcat -u host port
```

You can specify a range of ports by placing a dash between the first and last:

```
netcat host startport-endport
```


One of the most common uses for netcat is as a port scanner.

Although netcat is probably not the most sophisticated tool for the job (nmap is a better choice in most cases), it can perform simple port scans to easily identify open ports.

We do this by specifying a range of ports to scan, as we did above, along with the `-z` option to perform a scan instead of attempting to initiate a connection.

For instance, we can scan all ports up to 1000 by issuing this command:

```
netcat -z -v domain.com 1-1000
```
