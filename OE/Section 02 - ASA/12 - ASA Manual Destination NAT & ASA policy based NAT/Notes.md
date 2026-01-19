[Open: Pasted image 20260111094645.png](ec50d477022dc02012aa698682310ae0_MD5.jpeg)
![](ec50d477022dc02012aa698682310ae0_MD5.jpeg)

Destination and Policy NAT

R3 Outside - 192.1.1.24
R3 Inside - 172.16.1.2

Remote Outside IP - 2.2.2.1
Dummy Remote Outside IP - 172.16.1.80

Traffic sourced from 2.2.2.1 will be translated to 172.16.1.90 to be able to telnet to R3 Inside of 172.16.1.2

Create all 4 objects

```
object network R3-inside
	host 172.16.1.2
	
object network R3-outside
	host 192.1.1.24
	
outside-remote
	host 2.2.2.1

outside-dummy
	host 172.16.1.80
```

Manual destination NAT needs to be configured in the global policy, not in an object

```
nat (dmz,outside) source static R3-inside R3-outside dest static outside-dummy outside-remote
```

---

Policy NAT

Requirement - internal server 1 (10.20.10.1) needs to be translated to 192.1.1.40 when communicating with the 2.2.2.0/24 external network

Requirement - internal server 2 (10.20.20.1) needs to be translated to 192.1.1.41 when communicating with the 3.3.3.0/24 external network

Create network objects

```
object network internalserver1
	host 10.20.10.1
	
object network internalserver2
	host 10.20.20.1
	
object network public-server1
	host 192.1.1.40

object network public-server2
	host 192.1.1.41

object network EXT-2.2.2.0
	subnet 2.2.2.0 255.255.255.0
	
object network EXT-3.3.3.0
	subnet 3.3.3.0 255.255.255.0

```

This translation will need to go in the global nat policy

```
nat (inside,outside) source static internalserver1 public-server1 destination static EXT-2.2.2.0 EXT-2.2.2.0

nat (inside,outside) source static internalserver2 public-server2 destination static EXT-3.3.3.0 EXT-3.3.3.0
```

```
R1#ping 2.2.2.1 source lo1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2.2.2.1, timeout is 2 seconds:
Packet sent with a source address of 10.20.10.1 
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 1/1/2 ms
R1#ping 3.3.3.1 source lo2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 3.3.3.1, timeout is 2 seconds:
Packet sent with a source address of 10.20.20.1 
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 1/1/1 ms
R1#
```

```
ciscoasa(config)# show xlate
11 in use, 11 most used
Flags: D - DNS, e - extended, I - identity, i - dynamic, r - portmap,
       s - static, T - twice, N - net-to-net
NAT from DMZ:172.16.1.2 to outside:192.1.1.24
    flags s idle 0:59:34 timeout 0:00:00
NAT from DMZ:172.17.30.1 to outside:192.1.1.70
    flags s idle 0:59:34 timeout 0:00:00
NAT from DMZ:172.17.31.1 to outside:192.1.1.71
    flags s idle 0:59:34 timeout 0:00:00
TCP PAT from DMZ:172.17.32.1 23-23 to outside:192.1.1.80 50-50
    flags sr idle 0:59:34 timeout 0:00:00
TCP PAT from DMZ:172.17.33.1 23-23 to outside:192.1.1.80 51-51
    flags sr idle 0:59:34 timeout 0:00:00
NAT from DMZ:172.16.1.2 to outside:192.1.1.24
    flags sT idle 0:28:02 timeout 0:00:00
NAT from outside:2.2.2.1 to DMZ:172.16.1.80
    flags sT idle 0:28:02 timeout 0:00:00
NAT from inside:10.20.10.1 to outside:192.1.1.40
    flags sT idle 0:00:14 timeout 0:00:00
NAT from outside:2.2.2.0/24 to inside:2.2.2.0/24
    flags sIT idle 0:00:14 timeout 0:00:00
NAT from inside:10.20.20.1 to outside:192.1.1.41
    flags sT idle 0:00:02 timeout 0:00:00
NAT from outside:3.3.3.0/24 to inside:3.3.3.0/24
    flags sIT idle 0:00:02 timeout 0:00:00

ciscoasa(config)# 

ciscoasa(config)# show nat detail

Manual NAT Policies (Section 1)
1 (DMZ) to (outside) source static R3-inside R3-outside  destination static outside
-dummy outside-remote
    translate_hits = 2, untranslate_hits = 2
    Source - Origin: 172.16.1.2/32, Translated: 192.1.1.24/32
    Destination - Origin: 172.16.1.80/32, Translated: 2.2.2.1/32
2 (inside) to (outside) source static internalserver1 public-server1  destination s
tatic EXT-2.2.2.0 EXT-2.2.2.0
    translate_hits = 2, untranslate_hits = 2
    Source - Origin: 10.20.10.1/32, Translated: 192.1.1.40/32
    Destination - Origin: 2.2.2.0/24, Translated: 2.2.2.0/24
3 (inside) to (outside) source static internalserver2 public-server2  destination s
tatic EXT-3.3.3.0 EXT-3.3.3.0
    translate_hits = 1, untranslate_hits = 1
    Source - Origin: 10.20.20.1/32, Translated: 192.1.1.41/32
    Destination - Origin: 3.3.3.0/24, Translated: 3.3.3.0/24

Auto NAT Policies (Section 2)
1 (DMZ) to (outside) source static R3 192.1.1.24 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 172.16.1.2/32, Translated: 192.1.1.24/32
2 (DMZ) to (outside) source static accountingserver 192.1.1.70 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 172.17.30.1/32, Translated: 192.1.1.70/32
3 (DMZ) to (outside) source static salesforceserver 192.1.1.71 
    translate_hits = 0, untranslate_hits = 0
<--- More --->
    Source - Origin: 172.17.30.1/32, Translated: 192.1.1.70/32
3 (DMZ) to (outside) source static salesforceserver 192.1.1.71 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 172.17.31.1/32, Translated: 192.1.1.71/32
4 (DMZ) to (outside) source static payrollserver 192.1.1.80  service tcp telnet 50 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 172.17.32.1/32, Translated: 192.1.1.80/32
    Service - Protocol: tcp Real: telnet Mapped: 50 
5 (DMZ) to (outside) source static crmserver 192.1.1.80  service tcp telnet 51 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 172.17.33.1/32, Translated: 192.1.1.80/32
    Service - Protocol: tcp Real: telnet Mapped: 51 
6 (inside) to (outside) source dynamic R1 interface 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 10.10.10.2/32, Translated: 192.1.1.1/24
7 (inside) to (outside) source dynamic INTNET_10.20.10.0 ISPPOOL 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 10.20.10.0/24, Translated: 192.1.1.3-192.1.1.20
8 (inside) to (outside) source dynamic INTNET_10.20.20.0 ISPPOOL 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 10.20.20.0/24, Translated: 192.1.1.3-192.1.1.20
9 (inside) to (outside) source dynamic INTNET_10.20.30.0 pat-pool ISPPOOL_DynamicPAT
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 10.20.30.0/24, Translated (PAT): 192.1.1.21/32
10 (inside) to (outside) source dynamic INTNET_10.20.40.0 interface 
    translate_hits = 0, untranslate_hits = 0
    Source - Origin: 10.20.40.0/24, Translated: 192.1.1.1/24
ciscoasa(config)# 
```