# NAT Types

NAT Types
	Dynamic NAT (aka object nat, auto nat)
	Static NAT
	Dynamic PAT
	Static PAT
	Destination NAT
	Manual NAT / Twice NAT

In dynamic NAT / PAT it does not allow traffic to come from outside to inside (static can)

If internal IP is getting translated it's "source nat"

Check state / connection entry then NAT then ACLs. 

## Dynamic NAT
many to many
can use pool of ip's
ex inside to outside 
internal devices typically not aware
can be translated both directions
packet return - asa checks the nat table 

Syntax
```
object network [network name]
	range [start ip] [end ip] / subnet [subnet] [network mask] 
	nat (inside,outside) dynamic [pool name]
	
!!! Create pool
object network Public-Pool
	range 56.65.198.1 56.65.198.50
	
!!! Define Local pool
object network inside-clients
	subnet 10.10.10.0 255.255.255.0
	nat (inside,outside) dynamic Public-Pool
```

```
show users
show xlate
```

## Static NAT
one to one usually
bi directional translation

```
object network inside-clients
	subnet 10.10.10.0 255.255.255.0
	nat (inside,outside) dynamic external-ip
```

static nat immediately adds entry to translate tables

## Destination NAT
translates a remote device onto the local network
not commonly used

use when a local not routable device needs to communicate with a remote device
remote device ip translates to a local ip

Want remote IP (199.1.1.1) to communicate with a local router of 10.200.2.2 so you nat it as 10.200.2.254

First:

local router
```
object network local-router
	host 10.200.2.2
	nat(dmz,outside) static 202.263.96.10
```

Second:

remote router, coming in from outside, need to translate to a 10.200.2.254 so that it can talk to local router

```
object network remote-router
	host 199.1.1.1
	nat(outside,dmz) static 10.200.2.254
```

## Dynamic PAT
Multiple source IPs need to be translated to a single or pool of ips
ip/port combos kept in table 
port conflict resolution - can change source ports to ensure uniqueness

```
object network Inside-Hosts
	subnet 192.168.1.0 255.255.255.0
	nat(inside,outside) dynamic 202.100.234.123
```

Interface PAT
```
object network Inside-Hosts
	subnet 192.168.1.0 255.255.255.0
	nat(inside,outside) dynamic interface
```

PAT Pool
```
object network LAN
	subnet 10.1.1.0 255.255.255.0
	nat (inside,outside) dynamic pat-pool PATPOOL-GROUP
```

## Static PAT
port forwarding
internal devices need a fixed ip address on internet but have limited number of public ips.
ex access dmz webserver on the internet over port 443 - 1.1.1.1:443 
then access a different dmz smtp webserver over the same ip but different port 25 - 1.1.1.1:25

## Policy NAT
translate based on the flow of traffic
considers both source and destination
configured outside of objects in global config

```
object network remote-mf-private
	host 192.168.10.2

object network remote-mf-public
	host 59.234.123.153

object network local-mf-private
	host 10.1.1.2

object network local-mf-public
	host 209.234.201.123
	

nat (dmz,outside) source static local-mf-private local-mf-public destination static remote-mf-private remote-mf-public
```

# Ethertype ACLs
ACLs that specify an ethertype
16-bit hexadecimal 
implicit deny at end of ethertype acl does not affect ip traffic or arp
```
access-list ETHER ethertype permit 0x1234
access-list ETHER ethertype permit mpls-unicast

access-group ETHER in interface outside
```