[Open: Pasted image 20260429130257.png](../../../Media/10d840e96eb7f2b5332dd1c827b6f34d_MD5.jpeg)
![](../../../Media/10d840e96eb7f2b5332dd1c827b6f34d_MD5.jpeg)

NTP - network time protocol

```
# Set time zone
clock timezone SYD 10

# Set ntp stratum
ntp master 1

# Confgure NTP authentication
ntp authenticate
ntp authentication-key 111 md5 Cisco123
ntp trusted-key 111
```

