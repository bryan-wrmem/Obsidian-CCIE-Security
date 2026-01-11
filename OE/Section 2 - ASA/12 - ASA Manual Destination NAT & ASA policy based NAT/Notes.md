[Open: Pasted image 20260111094645.png](../../../Media/ec50d477022dc02012aa698682310ae0_MD5.jpeg)
![](../../../Media/ec50d477022dc02012aa698682310ae0_MD5.jpeg)

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
