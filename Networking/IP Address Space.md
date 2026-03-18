

# IPv4 Private Address Space and Filtering

According to standards set forth in Internet Engineering Task Force (IETF) document [RFC-1918](http://datatracker.ietf.org/doc/html/rfc1918) , the following IPv4 address ranges are reserved by the IANA for private internets, and are _not_ publicly routable on the global internet:

- **10.0.0.0/8 IP addresses:** 10.0.0.0 – 10.255.255.255
- **172.16.0.0/12 IP addresses:** 172.16.0.0 – 172.31.255.255
- **192.168.0.0/16 IP addresses:** 192.168.0.0 – 192.168.255.255

## Broadcast Address
from: https://www.ionos.com/digitalguide/server/know-how/broadcast-address/
the broadcast address can be used to send data packets in IP [networks](https://www.ionos.com/digitalguide/server/know-how/what-is-a-network/ "What is a network?") to all participants of a local network. The individual addresses of each party in the network do not have to be known for this to work. If necessary, the broadcast address can be calculated quite easily.