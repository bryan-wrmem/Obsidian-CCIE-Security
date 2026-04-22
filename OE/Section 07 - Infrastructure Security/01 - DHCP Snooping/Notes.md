![](Pasted%20image%2020260421204642.png)

Importance of DHCP snooping

Prevents rogue/untrusted dhcp servers from handing out IP addresses to clients

LAN Switch Config (main core)

```
# Globally enabled for "non-vlan" based traffic

ip dhcp snooping

# Enabled on vlan 10

ip dhcp snooping vlan 10

# Note - all dhcp will stop functioning unless we add trusted interface, interfaces that go to the authorized dhcp server



```