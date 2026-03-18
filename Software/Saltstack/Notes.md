from: https://www.youtube.com/watch?v=Dkd51QlNmO0

**Basic Salt Command**
![[Pasted image 20240430102157.png]]

- Declarative templating
	- States rather then instruction

A salt command goes out to every minion and the minion determines whether is matches the targeting value.
### Grains
Attributes of a minion. Many of these are gathered automatically by salt.
Grains are a keyvalue store, stored on the minion.
- Hostname
- OS
- OS Family

### Pillars
Minion data that is stored on the master.
- Highly sensitive data
- Arbitrary data
- Variables

### Mine
Minion data for other minions.
- Data for minions 
- Arbitrary data

example:
- You have a server that starts itself up, It then adds its own ip to the mine. The loadbalancer references the salt mine!

### Beacons/Reactors
Minion responds to events automatically
![[Pasted image 20240430104041.png]]


### Proxy Minions
Minions need python. Proxy minions allow for using a proxy to apply state through ssh or an api.



**Commands**

```
sudo salt 'cultivator-51-*' grains.items
```
List all the grains for a minion

```
sudo salt 'cultivator-51-*' pillar.items
```
List all the pillars that a minion has access to
