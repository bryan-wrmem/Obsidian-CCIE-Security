# Lab

Configure ASDM Management (easier for anyconnect and ssl vpns)
Note: eve-ng asdm interface is bridged to local home network, get ip from dhcp

```
conf t
int management 0/0
	ip address dhcp
	nameif Mgmt
	no shut

# create user for asdm

username bryan password cisco priv 15

# enable web server, allow management traffic

http server enable
http 0.0.0.0 0.0.0.0 Mgmt
	
```