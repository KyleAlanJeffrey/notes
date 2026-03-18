
Every device on the internet has an IP address. This address must be unique, there can be no two devices with the same IP. The number of IP addresses is limited, and mostly used up. There is a group of addresses that have been reserved for use only in internal networks. This works because the devices sharing an address cannot see each other - they are on different networks with no route between them.

Nat is implemented by a device (a computer, a router, or a firewall) that has two network connections, one to the internal network, one to the internet. When a device on the internal network wants to connect outside, it sends its messages (packets) to the NAT device. The NAT device strips the address of the original device and substitutes its own, then sends it out to the internet.

When the reply comes back, the NAT device then strips its own address, substitutes the address of the original device, and sends it to the internal network.

In this way, many devices can share one IP address.

