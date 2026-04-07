Configure AAA on SW-DHCP

```
aaa new-model

radius server ISE
	address ipv4 10.254.254.21 auth-port 1812 acct-port 1813
	key cisco123

aaa group server radius ISE-Server
	server name ISE


# Send RADIUS attributes

radius-server attribute 6 on-for-login-auth
radius-server attribute 8 include-in-access-req
radius-server attribute 25 access-request include

```