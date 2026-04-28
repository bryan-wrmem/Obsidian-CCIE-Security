IP spoofing is a method of attack by sending packets to a target network while hiding the attacker's address using a false source address.Thus, to achieve anti-spoofing using the access list, you need to create deny statements for each communication based on whether a valid sender address is specified.

First, drop the communications from private addresses defined in RFC1918.These addresses cannot be routed on the Internet, so it cannot come from outside as valid communications.

```
Router(config)# ip access-list extended anti-spoof
Router(config-ext-nacl)# deny ip 10.0.0.0 0.255.255.255 any
Router(config-ext-nacl)# deny ip 172.16.0.0 0.15.255.255 any
Router(config-ext-nacl)# deny ip 192.168.0.0 0.0.255.255 any
```

127.0.0.0/8 is a loopback address defined in RFC3330 and reserved for communications from each terminal to themselves.It cannot be transmitted from outside a terminal.

```
Router(config-ext-nacl)# deny ip 127.0.0.0 0.255.255.255 any
```

Finally, apply the created access list to the interface for Internet.

```
Router(config)# interface gigabitEthernet0/0

Router(config-if)# ip access-group anti-spoof in
```

