# Table of Contents
[Open: Pasted image 20260208091415.png](../../../Media/6468142a271cbcbe2c5d1bee12064209_MD5.jpeg)
![](../../../Media/6468142a271cbcbe2c5d1bee12064209_MD5.jpeg)

Tips & Tricks for the exam
Example 1
You may see a task that says

Create an IPSEC VPN between R1 and R2
Preshare key C!sC0123
name your transform set CiscoTS esp-sha esp-sha-hmac
make sure policy number is 100
crypto-map should be named as CiscoCMAP

If it doesn't say use ikev2, assume ikev1
Follow all instructions EXACTLY, case of names, numbers, etc. all need to match exactly
Copy and paste as much as possible from things like notepad to keep things the same
Can also use notepad to create configs to copy and paste across multiple devices to save time

---

Example 2
Task asks to create two anyconnect profiles - sales and hr
Sales profile should named as Sales_Cisco_prof and HR should be named HR_Cisco_prof
Create a certificate named ciscoasa and use encryption 2048
ensure that your anyconnect vpn is split tunnel and running IKE/IPSEC 