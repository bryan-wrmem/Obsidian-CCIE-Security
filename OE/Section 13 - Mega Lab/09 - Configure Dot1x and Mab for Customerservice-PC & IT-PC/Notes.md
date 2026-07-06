Switch Config

```
ip dhcp excluded-address 10.10.10.1
ip dhcp excluded-address 10.20.20.1

ip dhcp pool CS
 network 10.10.10.0 255.255.255.0
 default-router 10.10.10.1
!
ip dhcp pool IT
 network 10.20.20.0 255.255.255.0
 default-router 10.20.20.1

dot1x system-auth-control

interface Ethernet0/1
 no shutdown
 switchport access vlan 20

interface Ethernet0/2
 no shutdown
 switchport access vlan 10

interface Ethernet0/0
 no shutdown
 switchport access vlan 100
 switchport mode access
 duplex auto

interface Vlan10
 no shutdown
 ip address 10.10.10.1 255.255.255.0
!
interface Vlan20
 no shutdown
 ip address 10.20.20.1 255.255.255.0
!
interface Vlan100
 no shutdown
 ip address 192.168.0.248 255.255.255.0

aaa new-model
aaa group server radius ISE-SVRS
 server name ISE1
!
aaa authentication dot1x default group ISE-SVRS
aaa authorization network default group ISE-SVRS
dot1x system-auth-control

radius server ISE1
 address ipv4 192.168.0.249 auth-port 1812 acct-port 1813
 key Cisco123

ip route 0.0.0.0 0.0.0.0 192.168.0.254
!
interface Ethernet0/1
 no shutdown
 switchport access vlan 20
 switchport mode access
 duplex auto
 authentication order mab dot1x
 authentication priority mab dot1x
 authentication port-control auto
 mab
 dot1x pae authenticator
!
interface Ethernet0/2
 no shutdown
 switchport access vlan 10
 switchport mode access
 duplex auto
 authentication order dot1x mab
 authentication priority dot1x mab
 authentication port-control auto
 mab
 dot1x pae authenticator
!
```