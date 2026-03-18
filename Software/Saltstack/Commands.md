#### Salt Call

Pull a state from the salt master
```
sudo salt-call --master salt-dev.stoutagtech.com  -l debug state.apply
```

Apply all gateway states including Debian packages for minion  
```
sudo salt-call --master salt-dev.stoutagtech.com  -l debug state.apply appareo
```

Apply only gateway and minion-specific state, e.g., Debian packages. 
```
sudo salt-call --master salt-dev.stoutagtech.com  -l debug state.apply appareo.minion
```  

Apply multiple states to Gateway. 
```
sudo salt-call --master salt-dev.stoutagtech.com  -l debug state.apply appareo.minion,appareo.gateway
```  

#### Salt Push

Push a `vision.weights` state to cultivator 0
```
salt 'cultivator-0-camera-0' -l debug state.apply vision.weights
```

Push all state to cultivator 1
```
sudo salt 'cultivator-1-*' -l debug state.apply
```

#### Salt Testing

Render sls file
```
sudo salt 'cultivator-1-c*' state.show_sls tx2.logging
```

Runs through rendering to assure templating is correct. Does not call any state functions
```
sudo salt 'cultivator-1-*' state.apply mock=True
```

Runs full salt stack but will not actually apply state.
```
sudo salt 'cultivator-1-*' state.apply test=True
```

#### Salt Jobs

See active jobs
```
 salt-run jobs.active
```

Lookup job by id
```
salt-run jobs.lookup_jid <job id number>
```

See all jobs historic
```
salt-run jobs.list_jobs
```

kill job
```
sudo salt "cultivator-6-c*" saltutil.kill_job 20240319185301801156
```
#### Salt Kill



### [Accepting keys](https://docs.saltproject.io/salt/install-guide/en/latest/topics/accept-keys.html#accepting-keys "Permalink to this heading")

When a new minion checks in, the key will wait in `Unaccepted keys` until it is accepted.

Call `salt-key` to see the current state of key management:
```
salt-key
```

In this example, to accept keys, run:
```
salt-key -a db1
```

### Auxiliary Stuff
#### Some Helpful Comands
wipe all data on `/data`
```
sudo salt 'cultivator-x-c*' cmd.run 'systemctl stop disk-monitor cultivator-vision metadata-client shipper nginx && umount /dev/sda1 && mkfs.ext4 -F /dev/sda1 && reboot'
```

`sudo salt 'cultivator-x-c*' cmd.run 'systemctl stop shipper'`  
`sudo salt 'cultivator-x-*' state.apply cache`  
``  
`sudo salt 'cultivator-x-c*' cmd.run 'systemctl stop disk-monitor cultivator-vision metadata-client shipper nginx'`  
`sudo salt 'cultivator-x-c*' cmd.run 'apt purge -y aravis && apt purge -y cultivator-vision && apt purge -y disk-monitor && apt purge -y shipper && dpkg -P metadata-client && apt purge -y model && apt autoremove -y'`  
`sudo salt 'cultivator-x-c*' cmd.run 'cd /opt/stout/ && apt install -y ./aravis.deb'`  
`sudo salt 'cultivator-x-c*' state.apply`  
`sudo salt 'cultivator-x-c*' cmd.run 'systemctl enable disk-monitor cultivator-vision metadata-client shipper nginx && systemctl start disk-monitor cultivator-vision metadata-client shipper nginx'`  
`sudo salt 'cultivator-x-c*' cmd.run 'systemctl status disk-monitor cultivator-vision metadata-client shipper nginx | grep -i active'`  
`sudo salt 'cultivator-x-c*' cmd.run 'dpkg -l aravis && dpkg -l cultivator-vision && dpkg -l disk-monitor && dpkg -l shipper && dpkg -l metadata-client && dpkg -l model'`
