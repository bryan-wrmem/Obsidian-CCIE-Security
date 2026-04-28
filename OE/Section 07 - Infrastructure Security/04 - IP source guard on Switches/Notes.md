# IP Source Guard

Used on L2 interfaces. Filters traffic based on dhcp/arp inspection. Only allow traffic from IPs that are learned by dhcp snooping and arp inspection.

https://www.cisco.com/c/en/us/td/docs/switches/lan/c9000/sec-crypto/fhs-sisf/fhs-and-sisf-configuration-guide/ip-source-guard.html

IP Source Guard is a security feature that restricts IP traffic on nonrouted Layer 2 interfaces by filtering traffic based on the DHCP snooping binding database and on manually configured IP source bindings.

You can enable IP source guard when DHCP snooping is enabled. This ensures that IP traffic with a source IP address in the binding table is allowed, while all other traffic is denied.

The switch utilizes a source IP lookup table enabling both IP and MAC filtering through a combination of source IP and source MAC lookups. This table, known as the IP source binding table, contains bindings that are either learned by DHCP snooping or manually configured as static IP source bindings. Each entry in this table consists of an IP address, its associated MAC address, and its associated VLAN number.

IP source guard is supported on private VLAN access port and etherchannel but not on private VLAN trunk port. You have the capability to configure IP Source Guard with source IP address filtering or with source IP and MAC address filtering.

```
int e1/0
	ip verify source
```

