# Notes

[Open: Pasted image 20260119100510.png](../../../Media/dbcd6ce1f98e6de4c8cd5c0be799a098_MD5.jpeg)
![](../../../Media/dbcd6ce1f98e6de4c8cd5c0be799a098_MD5.jpeg)

Active/Active only supported in multi context mode

Create multiple contexts, i.e. HR-Context and IT-Context

ASA1 is active for the HR-Context, standby for Marketing
ASA2 is active for Marketing-Context, standby for HR

This way both ASAs are "active" and passing traffic

# Lab

[Open: Pasted image 20260119100615.png](../../../Media/be4157d420a6aa4ecd023cfa236ad478_MD5.jpeg)
![](../../../Media/be4157d420a6aa4ecd023cfa236ad478_MD5.jpeg)

Note: Use same interface for both LAN/STATE (eth3)

```
# create Mark context, allocate interfaces

context mark
	allocate-interface eth2 inside
	allocate-interface eth0 outside
	config-url flash:mark.cfg
	

# create HR context, allocate interfaces

context hr
	allocate-interface eth1 inside
	allocate-interface eth0 outside
	config-url flash:hr.cfg
	

# changeto contexts and configure interfaces

changeto context mark
int inside
	ip address 172.16.1.1 255.255.255.0 standby 172.16.1.2
	nameif Inside
	no shut

int outside
	ip address 1.1.1.1 255.255.255.0 standby 1.1.1.2
	nameif Outside
	no shut
	
changeto context hr
int inside
	ip address 172.16.2.1 255.255.255.0 standby 172.16.2.2
	nameif Inside
	no shut

int outside
	ip address 1.1.1.1 255.255.255.0 standby 1.1.1.2
	nameif Outside
	no shut
	

```