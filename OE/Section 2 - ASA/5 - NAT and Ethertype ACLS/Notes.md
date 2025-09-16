### NAT Types

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

