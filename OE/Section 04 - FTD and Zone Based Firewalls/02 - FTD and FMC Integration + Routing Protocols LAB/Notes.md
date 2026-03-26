[Open: Pasted image 20260326102219.png](../../../Media/e10e54b7bcbbf760139e78a343faeaeb_MD5.jpeg)
![](../../../Media/e10e54b7bcbbf760139e78a343faeaeb_MD5.jpeg)

Register ftd to fmc

[Open: Pasted image 20260326103327.png](../../../Media/0cf7f8ee878d574d26b9eff3ec92e709_MD5.jpeg)
![](../../../Media/0cf7f8ee878d574d26b9eff3ec92e709_MD5.jpeg)

[Open: Pasted image 20260326103358.png](../../../Media/bc8169a48971c6c787e9688aaaac7dc8_MD5.jpeg)
![](../../../Media/bc8169a48971c6c787e9688aaaac7dc8_MD5.jpeg)

[Open: Pasted image 20260326103513.png](../../../Media/085e2f0f583783c710cbca1cf6af12c8_MD5.jpeg)
![](../../../Media/085e2f0f583783c710cbca1cf6af12c8_MD5.jpeg)

Lab notes - use dynamic routing from FTD to routers

R1 - EIGRP
R2 - OSPF
R3 - BGP

create loopbacs to simulate remote network

R1 Lo1 - 10.40.40.1/24
R2 Lo1 - 10.20.10.1/24
R3 Lo1 - 10.30.30.1/24

Routing config

```
R1

router eigrp 100
 network 10.20.20.0 0.0.0.255
 network 10.40.40.0 0.0.0.255
 
R2

router ospf 1
 router-id 0.0.0.2
 network 10.10.10.0 0.0.0.255 area 0
 network 10.20.10.0 0.0.0.255 area 0
 
R3

router bgp 65534
 bgp log-neighbor-changes
 network 10.30.30.0 mask 255.255.255.0
 neighbor 11.11.11.1 remote-as 65530

```

FTD Config

Interfaces

[Open: Pasted image 20260326104254.png](../../../Media/cd323ee86b1f030cf56f558f352c3f7c_MD5.jpeg)
![](../../../Media/cd323ee86b1f030cf56f558f352c3f7c_MD5.jpeg)

Routing

EIGRP

[Open: Pasted image 20260326110010.png](../../../Media/fece8a96ebe991d3366d8df710eeeb8e_MD5.jpeg)
![](../../../Media/fece8a96ebe991d3366d8df710eeeb8e_MD5.jpeg)

[Open: Pasted image 20260326105829.png](../../../Media/52b7338780c9e47ef2da0613acaf3536_MD5.jpeg)
![](../../../Media/52b7338780c9e47ef2da0613acaf3536_MD5.jpeg)

[Open: Pasted image 20260326110044.png](../../../Media/617a1ce6ff8cab6e3e080fa0e33bdd08_MD5.jpeg)
![](../../../Media/617a1ce6ff8cab6e3e080fa0e33bdd08_MD5.jpeg)
====

OSPF

[Open: Pasted image 20260326110207.png](../../../Media/ffb4fffb70d2501fe419cc65ff4f3d0f_MD5.jpeg)
![](../../../Media/ffb4fffb70d2501fe419cc65ff4f3d0f_MD5.jpeg)

