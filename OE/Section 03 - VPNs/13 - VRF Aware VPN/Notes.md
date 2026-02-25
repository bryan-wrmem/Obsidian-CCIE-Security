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

