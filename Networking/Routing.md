
## Routing in Linux
Use `route` or `netstat -r` to view routing table definition on a router.

Example Route Table:
![[Pasted image 20240218131239.png]]

The **Destination** is where an ip request is trying to go.
The **Gateway** is the router to use to get there.
The **Genmask** is the 

0.0.0.0 is the **DEFAULT** route. All unmatched routes will fall into this route.

If the DEFAULT route is set for the Gateway, send the request direct.