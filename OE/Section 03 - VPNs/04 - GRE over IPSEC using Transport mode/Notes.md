# Lab

[Open: Pasted image 20260217193143.png](../../../Media/ccec6f0e44d69a2306eb745d23392819_MD5.jpeg)
![](../../../Media/ccec6f0e44d69a2306eb745d23392819_MD5.jpeg)

mode we configured in the last lab: tunnel mode

Other mode - Transport Mode

Encapsulates only the payload (data), leaving the original IP header intact.

Use **Transport Mode** when both endpoints are performing encryption/decryption directly (like two servers) or when using another encapsulation protocol (like GRE) where the IPsec is simply adding encryption to an already tunneled packet.

Saudi Arabia config

```
crypto ipsec transform-set TS esp-aes esp-sha-hmac
	mode transport
```

Australia config

```
crypto ipsec transform-set TS esp-aes esp-sha-hmac
	mode transport
```


