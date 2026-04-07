```
# Enable dot1x auth/authz

aaa authentication dot1x default group ISE-Server
aaa authorization network default group ISE-Server


dot1x system-auth-control
```

Configure dot1x on switchports

```
int e0/0

switchport mode access
switchport access vlan 10
authentication port-control auto
authentication order dot1x mab
authentication priority dot1x mab
dot1x pae authenticator
no shut

int e0/1

switchport mode access
switchport access vlan 20
authentication port-control auto
authentication order dot1x mab
authentication priority dot1x mab
dot1x pae authenticator
no shut
```

Create local ISE users

[Open: Pasted image 20260407091010.png](../../../Media/74988ea0a42a9d26210b4a6738abb418_MD5.jpeg)
![](../../../Media/74988ea0a42a9d26210b4a6738abb418_MD5.jpeg)

