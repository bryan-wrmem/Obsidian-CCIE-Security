FC and DS will show the following when managed by a SMC

[Open: Pasted image 20260507184509.png](../../../Media/508afb4baaae36c1d884036f86af761c_MD5.jpeg)
![](../../../Media/508afb4baaae36c1d884036f86af761c_MD5.jpeg)

Follow link to central management

[Open: Pasted image 20260507184610.png](../../../Media/414e239a51089059a4449631bec2dbef_MD5.jpeg)
![](../../../Media/414e239a51089059a4449631bec2dbef_MD5.jpeg)

Enable SSH on smc. SSH to smc with sysadmin account. Walk through wizard to enable initialize datastores

[Open: Pasted image 20260507191017.png](../../../Media/d4346d30185ee72e792ef9c637462ddb_MD5.jpeg)
![](../../../Media/d4346d30185ee72e792ef9c637462ddb_MD5.jpeg)

[Open: Pasted image 20260507191850.png](../../../Media/ae09bb905dfc1b8c56b0c23034cf0321_MD5.jpeg)
![](../../../Media/ae09bb905dfc1b8c56b0c23034cf0321_MD5.jpeg)

Router Config

```
# Configure flow record

flow record SNA-NETFLOW
  description NetFlow record format to send to FC
  match ipv4 tos
  match ipv4 protocol
  match ipv4 source address
  match ipv4 destination address
  match transport source-port
  match transport destination-port
  match interface input
  match flow direction
  collect routing source as
  collect routing destination as
  collect routing next-hop address ipv4
  collect ipv4 dscp
  collect ipv4 id
  collect ipv4 source prefix
  collect ipv4 source mask
  collect ipv4 destination mask
  collect ipv4 ttl minimum
  collect ipv4 ttl maximum
  collect transport tcp flags
  collect interface output
  collect counter bytes
  collect counter packets
  collect timestamp sys-uptime first
  collect timestamp sys-uptime last

# =======
# Configure flow exporter

flow exporter NETFLOW_FC
  description Export NetFlow to SW FC
  destination 10.253.253.43
  transport udp 2055
  template data timeout 30
  export-protocol ipfix
  
# =======
# Configure flow monitor

flow monitor IPv4_NETFLOW
  record SNA-NETFLOW
  exporter NETFLOW_FC
  cache timeout active 60
  cache timeout inactive 15

# =======
# enable flow monitor on interfaces

interface range Ethernet0/0-3
  ip flow monitor IPv4_NETFLOW input


```