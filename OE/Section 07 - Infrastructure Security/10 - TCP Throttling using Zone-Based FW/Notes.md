# TCP Throttling

TCP 3 Way Handshake

The TCP 3-way handshake is ==a process used in TCP/IP networks to establish a reliable, connection-oriented session between a client and a server before data transfer==. It involves three steps—**[SYN](https://www.google.com/search?client=firefox-b-1-d&q=SYN&mstk=AUtExfBeoPpQ06TWyT88GiBsJxi39XfvApLmk1Cmye_qSuq2X5wNwW-17uvoCsYeqxTuoqwpket_uvc9zZXQP0Kb0hmUgjmDJ3OWhQd1uJSd_sEV3BpZbmvgGdsLjMLvji5s3iA&csui=3&ved=2ahUKEwiDkLbPoJmUAxUMMlkFHXl6HnUQgK4QegYIAggAEA8), SYN-ACK, ACK**—ensuring both parties are synchronized, sequence numbers are exchanged, and connections are established, allowing bidirectional communication. [[1](https://www.geeksforgeeks.org/computer-networks/tcp-3-way-handshake-process/), [2](https://www.akamai.com/blog/security/tcp-three-way-handshake), [3](https://networkwalks.com/tcp-3-way-handshake-process/)]

[TCP throttling in a Zone-Based Firewall (ZBF)](https://www.google.com/search?client=firefox-b-1-d&q=TCP+throttling+in+a+Zone-Based+Firewall+%28ZBF%29&mstk=AUtExfAqHrz9qTg62cstmuAJfJ8v-Xwiw8l4ORB4Lf5urZf7IZGtDTxAeI15MptDGPrMIZHJ78q2ql54d08NGjBKuD6D9ovmMLFu-6USMG7P390WvRkJ09lfxz2E07iy2MKP1vLptA31WmjIvoRWsnlDn-Vk60gW6rcG2kv9n-EoA7x5C8klg_4jjDw1NwpR5bmAruNI5Kx_hEK5fHj-VF8IDi-WptIUHqB1rOnFO19y3jd7TKeK-gEBhAay3w8d04G7mI-pmaUQimBWDBKmp1uVfT3sdzW113ojXzLhUfNNy9hTfJhb7jIuVesvYo4il8hFNjPUv6zFrb-EYVoIQ0bzil9UN1BqMCHMAEYOAfrEe4HH&csui=3&ved=2ahUKEwjrs8jToZmUAxVGGlkFHdr4Ek8QgK4QegQIARAB) (such as on Cisco IOS/IOS XE) ==involves controlling the rate, volume, or connection state of TCP traffic passing between security zones== (e.g., from a `TRUSTED` zone to an `UNTRUSTED` zone). ZBF uses class maps to match traffic and policy maps to apply actions like inspection, dropping, or limiting. [[1](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/sec_data_zbf/configuration/xe-16/sec-data-zbf-xe-16-book/sec-loose-checking-option-TCP.html), [2](https://www.dclessons.com/zone-based-firewalls)]

Configure Router for ZBF

```
zone security outside
	description outside traffic
	
int e0/0
	zone-member security outside
	
# no rules setup, so traffic will be auto dropped

# create paramter map for tcp inspection

parameter-map type INSPECT TCP
	alert on
	max-incomplete low 2
	max-incomplete high 6
	
# create acl

ip access-list extended FROM-SOURCE
permit tcp any host 23.1.1.2 eq 80

class-map type inspect match-all CMAP
	match access-group name FROM-SOURCE
	match protocol http
	
policy-map type inspect PMAP
	class type inspect CMAP
	inspect TCP
	class class-default 
	pass
	
policy-map type inspect PMAP-SELF
	class class-default
	pass

zone-pair security OUTSIDE source outside destination self
	service-policy type inspect PMAP
	
zone-pair security ZP-SELFOUT source self destination outside
	service-plicy type inspect PMAP-SELF
```