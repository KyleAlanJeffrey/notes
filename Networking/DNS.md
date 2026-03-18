
## Some Notes from [Ben Eater](https://www.youtube.com/watch?v=-wMU8vmfaYo)

Everything begins with DNS root servers.

"*The authoritative name servers that serve the DNS root zone, commonly known as the “root servers”, are a network of hundreds of servers in many countries around the world. They are configured in the DNS root zone as 13 named authorities, as follows.*"
#### List of Root Servers
https://www.iana.org/domains/root/servers
|   |   |   |
|---|---|---|
|a.root-servers.net|198.41.0.4, 2001:503:ba3e::2:30|Verisign, Inc.|
|b.root-servers.net|170.247.170.2, 2801:1b8:10::b|University of Southern California,  <br>Information Sciences Institute|
|c.root-servers.net|192.33.4.12, 2001:500:2::c|Cogent Communications|
|d.root-servers.net|199.7.91.13, 2001:500:2d::d|University of Maryland|
|e.root-servers.net|192.203.230.10, 2001:500:a8::e|NASA (Ames Research Center)|
|f.root-servers.net|192.5.5.241, 2001:500:2f::f|Internet Systems Consortium, Inc.|
|g.root-servers.net|192.112.36.4, 2001:500:12::d0d|US Department of Defense (NIC)|
|h.root-servers.net|198.97.190.53, 2001:500:1::53|US Army (Research Lab)|
|i.root-servers.net|192.36.148.17, 2001:7fe::53|Netnod|
|j.root-servers.net|192.58.128.30, 2001:503:c27::2:30|Verisign, Inc.|
|k.root-servers.net|193.0.14.129, 2001:7fd::1|RIPE NCC|
|l.root-servers.net|199.7.83.42, 2001:500:9f::42|ICANN|
|m.root-servers.net|202.12.27.33, 2001:dc3::35|WIDE Project|

## Resolving IP Over the Internet
**Begin with DNS resolution**:
There are 12 canonical root servers that maintain child nameservers that will connect a client through intermediary steps to a location.

![[Pasted image 20240124082046.png]]


Several other third party services host their own DNS name servers

|Provider|Primary DNS|Secondary DNS|
|---|---|---|
|[Google](https://developers.google.com/speed/public-dns/)|8.8.8.8|8.8.4.4|
|[Control D](https://controld.com/free-dns)|76.76.2.0|76.76.10.0|
|[Quad9](https://www.quad9.net/)|9.9.9.9|149.112.112.112|
|[OpenDNS Home](https://www.opendns.com/)|208.67.222.222|208.67.220.220|
|[Cloudflare](https://1.1.1.1/dns/)|1.1.1.1|1.0.0.1|
|[CleanBrowsing](https://cleanbrowsing.org/filters/)|185.228.168.9|185.228.169.9|
|[Alternate DNS](https://alternate-dns.com/)|76.76.19.19|76.223.122.150|
|[AdGuard DNS](https://adguard-dns.io/en/public-dns.html)|94.140.14.14|94.140.15.15|

**After DNS Resolution**
Once an IP address has been determined, your computer will go through a series of routing tables to get where it needs to go.