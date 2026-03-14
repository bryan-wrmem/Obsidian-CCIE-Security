[Open: Pasted image 20260314114551.png](../../../Media/e9bb3db8c1ba341bd62b362a494f6ad6_MD5.jpeg)
![](../../../Media/e9bb3db8c1ba341bd62b362a494f6ad6_MD5.jpeg)

Multipoint mappings. Melbourne will be the hub with SVTI interface. Riyadh and Perth will be spokes with DVTI interfaces. Multipoint will allow for spoke-to-hub, hub-to-spoke, and spoke-to-spoke traffic.

Melbourne as the hub will need nhrp/nhs to allow for spokes to resolve each other's IPs.
Hub - ip nhrp redirect
Spokes - ip nhrp shortcut

We can also have the hub assign tunnel ip's to the spokes. 
Create an ip pool on Hub.
192.168.1.15-20

```
# Melbourne  

# aaa config as the there is a crypto ikev2 authorization policy

aaa new-model
aaa authorization network default local
! 
crypto ikev2 authorization policy default
 pool DVPNtunnel
 route set interface
!
crypto ikev2 proposal PROPOSAL 
 encryption 3des aes-cbc-128
 integrity md5 sha1
 group 2 5
!
crypto ikev2 policy POLICY 
 proposal PROPOSAL
!
crypto ikev2 keyring MEL
 peer SPOKES
  address 0.0.0.0 0.0.0.0
  pre-shared-key mohsin123
 !
!
crypto ikev2 keyring SPOKES
 peer MEL
  address 0.0.0.0 0.0.0.0
  pre-shared-key mohsin123
 !
!
!
crypto ikev2 profile IKEV2-MEL
 match identity remote address 0.0.0.0 
 authentication remote pre-share
 authentication local pre-share
 keyring local MEL
 aaa authorization group override psk list default default
 virtual-template 1
!
crypto ikev2 profile IKEV2-SPK
 match identity remote address 0.0.0.0 
 authentication remote pre-share
 authentication local pre-share
 keyring local SPOKES
 aaa authorization group override psk list default default
 virtual-template 1
!
!
!
crypto ipsec transform-set TS esp-3des esp-sha-hmac 
 mode tunnel
!
crypto ipsec profile DVTIPROF
 set transform-set TS 
 set ikev2-profile IKEV2-MEL
!
!
!
!
interface Tunnel1
 no shutdown
 ip address negotiated
 ip nhrp network-id 1
 ip nhrp shortcut virtual-template 1
 tunnel source Ethernet0/0
 tunnel destination 3.3.3.2
 tunnel protection ipsec profile DVTIPROF
!
!
interface Virtual-Template1 type tunnel
 no shutdown
 ip unnumbered Loopback100
 ip nhrp network-id 1
 ip nhrp shortcut
 ip nhrp redirect
 tunnel source Ethernet0/0
 tunnel protection ipsec profile DVTIPROF
!
!
router eigrp 1
 network 172.16.5.0 0.0.0.255
 network 172.16.6.0 0.0.0.255
 network 192.168.1.0
!
ip local pool DVPNtunnel 192.168.1.15 192.168.1.20
!
interface Loopback100
 no shutdown
 ip address 192.168.1.4 255.255.255.0
!

interface Ethernet0/0
 no shutdown
 ip address 3.3.3.2 255.255.255.0
 duplex auto
!

# ======================

# Perth


!
! 
crypto ikev2 authorization policy default
 pool DVPNtunnel
 route set interface
!
crypto ikev2 proposal PROPOSAL 
 encryption 3des aes-cbc-128
 integrity md5 sha1
 group 2 5
!
crypto ikev2 policy POLICY 
 proposal PROPOSAL
!
crypto ikev2 keyring SPOKES
 peer MEL
  address 0.0.0.0 0.0.0.0
  pre-shared-key mohsin123
 !
!
!
!
crypto ikev2 profile IKEV2-SPK
 match identity remote address 0.0.0.0 
 authentication remote pre-share
 authentication local pre-share
 keyring local SPOKES
 aaa authorization group override psk list default default
 virtual-template 1
!
!
!
!
crypto ipsec transform-set TS esp-3des esp-sha-hmac 
 mode tunnel
!
crypto ipsec profile DVTIPROF
 set transform-set TS 
 set ikev2-profile IKEV2-SPK
 virtual-template 1
!
!
!
!
!
!
interface Ethernet0/0
 no shutdown
 ip address 4.4.4.2 255.255.255.0
 duplex auto
!
interface Tunnel1
 no shutdown
 ip address negotiated
 ip nhrp network-id 1
 ip nhrp shortcut virtual-template 1
 tunnel source Ethernet0/0
 tunnel destination 3.3.3.2
 tunnel protection ipsec profile DVTIPROF
!
interface Virtual-Template1 type tunnel
 no shutdown
 ip unnumbered Tunnel1
 ip nhrp network-id 1
 ip nhrp shortcut
 ip nhrp redirect
 tunnel source Ethernet0/0
 tunnel protection ipsec profile DVTIPROF
!
!
router eigrp 1
 network 172.16.7.0 0.0.0.255
 network 172.16.8.0 0.0.0.255
 network 192.168.1.0


# ============================

# Riyadh


!
multilink bundle-name authenticated
!
!
!
! 
crypto ikev2 authorization policy default
 route set interface
!
crypto ikev2 proposal PROPOSAL 
 encryption 3des aes-cbc-128
 integrity md5 sha1
 group 2 5
!
crypto ikev2 policy POLICY 
 proposal PROPOSAL
!
crypto ikev2 keyring SPOKES
 peer MEL
  address 0.0.0.0 0.0.0.0
  pre-shared-key mohsin123
 !
!
!
crypto ikev2 profile IKEV2-SPK
 match identity remote address 0.0.0.0 
 authentication remote pre-share
 authentication local pre-share
 keyring local SPOKES
 virtual-template 1
!
!
!
crypto ipsec transform-set TS esp-3des esp-sha-hmac 
 mode tunnel
!
crypto ipsec profile DVTIPROF
 set transform-set TS 
 set ikev2-profile IKEV2-SPK
 virtual-template 1
!
!
interface Ethernet0/0
 no shutdown
 ip address 2.2.2.2 255.255.255.0
 duplex auto
!
interface Loopback100
 no shutdown
 ip address 192.168.1.4 255.255.255.0
!
!
interface Tunnel1
 no shutdown
 ip address negotiated
 ip nhrp network-id 1
 ip nhrp shortcut virtual-template 1
 tunnel source Ethernet0/0
 tunnel destination 3.3.3.2
 tunnel protection ipsec profile DVTIPROF
!
!
interface Virtual-Template1 type tunnel
 no shutdown
 ip unnumbered Tunnel1
 ip nhrp network-id 1
 ip nhrp shortcut
 tunnel source Ethernet0/0
 tunnel protection ipsec profile DVTIPROF
!
!
router eigrp 1
 network 172.16.3.0 0.0.0.255
 network 172.16.4.0 0.0.0.255
 network 192.168.1.0
!
```