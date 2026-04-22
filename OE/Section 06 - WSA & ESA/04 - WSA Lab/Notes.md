# Lab

[Open: Pasted image 20260421185942.png](../../../Media/dc9136ffb446630b9b4f9c5c0bdcc927_MD5.jpeg)
![](../../../Media/dc9136ffb446630b9b4f9c5c0bdcc927_MD5.jpeg)

[Open: Pasted image 20260421185405.png](../../../Media/a86e82f6645d094dd248d103e8f1c457_MD5.jpeg)
![](../../../Media/a86e82f6645d094dd248d103e8f1c457_MD5.jpeg)

[Open: Pasted image 20260421185431.png](../../../Media/0a7f9fe1cf5695fa21279a13771a4333_MD5.jpeg)
![](../../../Media/0a7f9fe1cf5695fa21279a13771a4333_MD5.jpeg)

[Open: Pasted image 20260421185506.png](../../../Media/d424e3e1f623875c0897a34a25c3f3a1_MD5.jpeg)
![](../../../Media/d424e3e1f623875c0897a34a25c3f3a1_MD5.jpeg)

[Open: Pasted image 20260421185521.png](../../../Media/fb245a6ff09609a1f75c6c3f1e840838_MD5.jpeg)
![](../../../Media/fb245a6ff09609a1f75c6c3f1e840838_MD5.jpeg)

[Open: Pasted image 20260421185650.png](../../../Media/4921cd20afc67f160d26f2c17997e42a_MD5.jpeg)
![](../../../Media/4921cd20afc67f160d26f2c17997e42a_MD5.jpeg)

[Open: Pasted image 20260421185723.png](../../../Media/d47e39907c2e251cb3268d3df95570f8_MD5.jpeg)
![](../../../Media/d47e39907c2e251cb3268d3df95570f8_MD5.jpeg)

[Open: Pasted image 20260421185740.png](../../../Media/cb3dc4b0adb7c7ead18431584ff903ea_MD5.jpeg)
![](../../../Media/cb3dc4b0adb7c7ead18431584ff903ea_MD5.jpeg)

[Open: Pasted image 20260421185803.png](../../../Media/c0a5b23b551b54347dbdf285a7726d46_MD5.jpeg)
![](../../../Media/c0a5b23b551b54347dbdf285a7726d46_MD5.jpeg)

[Open: Pasted image 20260421190420.png](../../../Media/0f601cd41a06ab6307af58584d923916_MD5.jpeg)
![](../../../Media/0f601cd41a06ab6307af58584d923916_MD5.jpeg)

[Open: Pasted image 20260421190503.png](../../../Media/90cecf4375fd55a7f66f7de5af84bada_MD5.jpeg)
![](../../../Media/90cecf4375fd55a7f66f7de5af84bada_MD5.jpeg)

[Open: Pasted image 20260421190526.png](../../../Media/e0ba8d740961b69b61ba11d995c0758e_MD5.jpeg)
![](../../../Media/e0ba8d740961b69b61ba11d995c0758e_MD5.jpeg)

## Additional Settings to know for exam

Security Settings -> Web Proxy

May be asked to change HTTP Ports

[Open: Pasted image 20260421191426.png](../../../Media/e85db974798d89d555818cdc2c7f9bf4_MD5.jpeg)
![](../../../Media/e85db974798d89d555818cdc2c7f9bf4_MD5.jpeg)

## Configure WSA for WCCP

[Open: Pasted image 20260421193157.png](../../../Media/841ddc7ef255652556cc7d62fa4aa448_MD5.jpeg)
![](../../../Media/841ddc7ef255652556cc7d62fa4aa448_MD5.jpeg)

[Open: Pasted image 20260421193224.png](../../../Media/a56ca0dffcc226ad96d31c66bd3b3239_MD5.jpeg)
![](../../../Media/a56ca0dffcc226ad96d31c66bd3b3239_MD5.jpeg)

[Open: Pasted image 20260421193306.png](../../../Media/50f229e55af0284069be25c754542432_MD5.jpeg)
![](../../../Media/50f229e55af0284069be25c754542432_MD5.jpeg)

[Open: Pasted image 20260421193500.png](../../../Media/f735e80b9d4c8149a55355d7ec03e8a8_MD5.jpeg)
![](../../../Media/f735e80b9d4c8149a55355d7ec03e8a8_MD5.jpeg)

(wccp pass: cisco123)

[Open: Pasted image 20260421193552.png](../../../Media/59ece63a3c50e8d8180b5c2bddc3d67b_MD5.jpeg)
![](../../../Media/59ece63a3c50e8d8180b5c2bddc3d67b_MD5.jpeg)

## WCCP Config on SW/Router

```
! Access list to permit traffic to WSA
access-list 1 permit 10.254.254.33

! Access list for web traffic
access-list 102 permit tcp any any eq 80
access-list 102 permit tcp any any eq 443


ip wccp 1 redirect-list 102 group-list 1 password cisco123

! Configure WCCP Redirection

int vlan 10
ip wccp 1 redirect in

int vlan 20
ip wccp 1 redirect in
```

[Open: Pasted image 20260421200752.png](../../../Media/cd4ed7bf067de50379ca76b94469259f_MD5.jpeg)
![](../../../Media/cd4ed7bf067de50379ca76b94469259f_MD5.jpeg)

## Create differentiated policies based on identity/subnet

[Open: Pasted image 20260421201228.png](../../../Media/8137fd530b715e76ccabb2c9bbd9ea3a_MD5.jpeg)
![](../../../Media/8137fd530b715e76ccabb2c9bbd9ea3a_MD5.jpeg)

[Open: Pasted image 20260421201326.png](../../../Media/df86021a498626d85808555ba5c130dc_MD5.jpeg)
![](../../../Media/df86021a498626d85808555ba5c130dc_MD5.jpeg)

[Open: Pasted image 20260421201851.png](../../../Media/6359a0997a3d218b2364f7c65e263366_MD5.jpeg)
![](../../../Media/6359a0997a3d218b2364f7c65e263366_MD5.jpeg)

