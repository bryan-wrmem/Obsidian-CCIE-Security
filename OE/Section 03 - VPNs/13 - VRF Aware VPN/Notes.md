[Open: Pasted image 20260225085008.png](../../../Media/fbe7c6f09ed98eae7922803715756c62_MD5.jpeg)
![](../../../Media/fbe7c6f09ed98eae7922803715756c62_MD5.jpeg)

2 Sites - Melbourne and Sidney

Each site has an Accounting and HR Department. Accounting and HR are in two different VRFs - Accounting VRF (green), HR VRF (red).

SYD/MEL Configs

```
# Configure VRFs

ip vrf HR
ip vrf Accounting

# Configure Sub-interfaces on main routers

int e0/0
	no shut

int e0/0.1
	encapsulation dot1q 1
	ip vrf forwarding HR
	ip address 1.1.1.X 255.255.255.0
	
int e0/0.2
	encapsulation dot1q 2
	ip vrf fowarding Accounting
	ip address 2.2.2.X 255.255.255.0
	
# Configure Interfaces pointing to HR and Accounting

int e0/1
	ip vrf forwardng HR
	ip address 172.16.X.X 255.255.255.0
	
int e0/2
	ip vrf forwardng Accounting
	ip address 172.16.X.X 255.255.255.0
```

Configure routing protocols

MEL

```
router eigrp 1
 !
 address-family ipv4 vrf HR autonomous-system 1
  network 1.1.1.0 0.0.0.255
  network 172.16.10.0 0.0.0.255
 exit-address-family
!
router ospf 1 vrf Accounting
 network 2.2.2.0 0.0.0.255 area 0
 network 172.16.10.0 0.0.0.255 area 0
!
```

SYD

```
router eigrp 1
 !
 address-family ipv4 vrf HR autonomous-system 1
  network 1.1.1.0 0.0.0.255
  network 172.16.20.0 0.0.0.255
 exit-address-family
!
router ospf 1 vrf Accounting
 network 2.2.2.0 0.0.0.255 area 0
 network 172.16.20.0 0.0.0.255 area 0
!
```

Apply IPSec to the tunnels

Mel

```

# Configure phase 1

crypto isakmp policy 10
	auth pre-share
	encryption 3des
	hash md5
	group 2
	
# Configure pre-share key (different command due to vrfs)

crypto keyring keyring-HR vrf HR
	pre-shared-key address 0.0.0.0 key moshin123
	
crypto keyring keyring-Accounting vrf Accounting
	pre-shared-key address 0.0.0.0 key moshin123
	
# Apply keyring to isakmp profile

crypto isakmp profile PROF-HR
	vrf HR
	keyring keyring-HR
	match identity address 0.0.0.0 0.0.0.0 HR

crypto isakmp profile PROF-Accounting
	vrf Accounting
	keyring keyring-Accounting
	match identity address 0.0.0.0 0.0.0.0 Accounting
	
# Configure phase 2

crypto ipsec transform-set TS esp-3des esp-sha-hmac

crypto ipsec profile IPSECPROF
	set transform-set TS
	
# Create access-list and crypto map to apply to HR interface

access-list 102 permit ip 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255

crypto map C-HR isakmp-profile PROF-HR
crypto map C-HR 10 ipsec-isakmp
	match address 102
	set peer 1.1.1.2
	set transform-set TS

int e0/0.1
	crypto map C-HR


# Create access-list and crypto map to apply to Accounting interface

access-list 102 permit ip 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255

crypto map C-Accounting isakmp-profile PROF-Accounting
crypto map C-Accounting 10 ipsec-isakmp
	match address 102
	set peer 2.2.2.2
	set transform-set TS

int e0/0.2
	crypto map C-Accounting
	
```

SYD

```

# Configure phase 1

crypto isakmp policy 10
	auth pre-share
	encryption 3des
	hash md5
	group 2
	
# Configure pre-share key (different command due to vrfs)

crypto keyring keyring-HR vrf HR
	pre-shared-key address 0.0.0.0 key moshin123
	
crypto keyring keyring-Accounting vrf Accounting
	pre-shared-key address 0.0.0.0 key moshin123
	
# Apply keyring to isakmp profile

crypto isakmp profile PROF-HR
	vrf HR
	keyring keyring-HR
	match identity address 0.0.0.0 0.0.0.0 HR

crypto isakmp profile PROF-Accounting
	vrf Accounting
	keyring keyring-Accounting
	match identity address 0.0.0.0 0.0.0.0 Accounting
	
# Configure phase 2

crypto ipsec transform-set TS esp-3des esp-sha-hmac

crypto ipsec profile IPSECPROF
	set transform-set TS
	
# Create access-list and crypto map to apply to HR interface

access-list 102 permit ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255

crypto map C-HR isakmp-profile PROF-HR
crypto map C-HR 10 ipsec-isakmp
	match address 102
	set peer 1.1.1.1
	set transform-set TS

int e0/0.1
	crypto map C-HR


# Create access-list and crypto map to apply to Accounting interface

access-list 102 permit ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255

crypto map C-Accounting isakmp-profile PROF-Accounting
crypto map C-Accounting 10 ipsec-isakmp
	match address 102
	set peer 2.2.2.1
	set transform-set TS

int e0/0.2
	crypto map C-Accounting
	
```