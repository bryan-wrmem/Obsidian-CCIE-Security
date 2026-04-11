# DACLs
## Downloadable Access Control Lists

For example, when the sales user authenticates, ISE can push a DACL preventing it getting to certain resources. Only allow sales to talk to the sales network 10.10.10.0/24

permit ip any 10.10.10.0 255.255.255.0
deny ip any any


