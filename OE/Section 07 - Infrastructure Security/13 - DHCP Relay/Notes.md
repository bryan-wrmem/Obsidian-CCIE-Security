[Open: Pasted image 20260503095410.png](20e833dd38c3a7d3404209acd3a038e7_MD5.jpeg)
![](20e833dd38c3a7d3404209acd3a038e7_MD5.jpeg)

The Cisco `ip helper-address` command is used on a Layer 3 interface (router interface or SVI) to enable the DHCP relay agent functionality. It forwards DHCP broadcast requests from clients to a specific DHCP server located on a different subnet, transforming the broadcast into a unicast packet. [[1](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/12-2sx/dhcp-12-2sx-book/dhcp-relay-agent.html), [2](https://www.connecteddots.online/resources/cisco/ip-helper-address)]

**Key Details and Usage:**

- **Purpose:** Allows a centralized DHCP server to serve multiple subnets/VLANs, removing the need for a DHCP server on every segment.
- **Where to Apply:** Configure it on the "client-facing" interface (e.g., VLAN SVI or router interface) where the broadcast originates.
- **Functionality:** The router inserts the client's subnet IP address (gateway IP) into the DHCP packet, allowing the DHCP server to assign an appropriate address.
- **Multiple Servers:** Multiple `ip helper-address` commands can be applied to one interface for redundancy. [[1](https://community.cisco.com/t5/switching/placement-of-ip-helper-address/td-p/1880589), [2](https://www.cisco.com/en/US/docs/ios/12_4t/ip_addr/configuration/guide/htdhcpre.html), [3](https://www.connecteddots.online/resources/cisco/ip-helper-address), [4](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/12-2sx/dhcp-12-2sx-book/dhcp-relay-agent.html)]