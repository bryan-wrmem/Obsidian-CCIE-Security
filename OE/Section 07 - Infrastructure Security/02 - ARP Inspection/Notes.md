[Open: Pasted image 20260427190625.png](../../../Media/eb1c3a596e51f982db1a2c6c35174802_MD5.jpeg)
![](../../../Media/eb1c3a596e51f982db1a2c6c35174802_MD5.jpeg)

Help stop ARP Poisoning/spoofing attacks

ARP (Address Resolution Protocol) poisoning, also known as **ARP spoofing**, is a cyberattack where an attacker sends forged ARP messages over a local area network (LAN). The goal is to link the attacker's MAC address with the IP address of a legitimate device (usually the default gateway).


```
# command to create a static mac address/ip entry

ip source binding xxxx.xxxx.xxxx vlan 100 192.168.10.3 int e1/0
```
