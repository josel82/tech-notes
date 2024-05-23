# QoS Configuration

```
class-map TEST
	match dscp <0-63|default|ef|af11-43|cs1-7> 
```

##  RFC 4594 Recommendations

- Voice traffic -> EF
- Interactive video -> AF4x
- Streaming video -> AF3x
- High priority data -> AF2x
- Best effort -> DF


![Cisco Implementation of RFC 4594](https://ptgmedia.pearsoncmg.com/images/chap16_9781587144622/elementLinks/16fig04_alt.jpg)
[https://www.ciscopress.com/articles/article.asp?p=2756478&seqNum=7](https://www.ciscopress.com/articles/article.asp?p=2756478&seqNum=7)

## Trust boundary
 Trusted boundary uses CDP to detect the presence of a Cisco IP Phone (such as the Cisco IP Phone 7910, 7935, 7940, and 7960) on a device port.
```
R1(config-if)trust device <device_type>
```