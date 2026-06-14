```
# create HR context, allocate interfaces

context HR
	allocate-interface eth1 inside
	allocate-interface eth3 outside
	config-url flash:hr.cfg
	

# create ACC context, allocate interfaces

context ACC
	allocate-interface eth2 inside
	allocate-interface eth3 outside
	config-url flash:ACC.cfg
	

# changeto contexts and configure interfaces

changeto context HR
int inside
	ip address 172.16.1.1 255.255.255.0 standby 172.16.1.2
	nameif inside
	no shut

int outside
	ip address 1.1.1.1 255.255.255.0 standby 1.1.1.2
	nameif outside
	no shut


	
changeto context ACC
int inside
	ip address 172.16.2.1 255.255.255.0 standby 172.16.2.2
	nameif inside
	no shut

int outside
	# ip address needs to be unique, can't overlap with mark context IPs
	ip address 1.1.1.3 255.255.255.0 standby 1.1.1.4
	nameif outside
	no shut
	
=======

changeto context system

failover lan interface LAN eth0
failover interface ip LAN 7.7.7.1 255.255.255.0 7.7.7.2
failover lan unit primary
failover key cisco123
failover link ST eth0
failover

# on secondary

failover lan interface LAN eth0
failover interface ip LAN 7.7.7.7.1 255.255.255.0 7.7.7.2
failover lan unit secondary
failover key cisco123
failover link ST eth0
failover


# configure failover groups
failover group 1
primary
preempt

failover group 2
secondary
preempt

context mark
join-failover-group 1

context hr
join-failover-group 2
```