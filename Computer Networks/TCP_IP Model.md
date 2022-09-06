# TCP(Transmission Control Protocol)/ IP(Internet Protocol) Model

It is the compressed version of the OSI model with only 4 layers. It was developed by the US Department of Defence(DoD) in the 1860s. The name of this model is based on 2 standards protocol used i.e TCP(Transmission Control Protocol) and IP(Internet Protocol).

##### Four Layers :
1. **Application :** It contains all the higher-level protocol. Ex- HTTP, SMTP, RTP
2. **Transport :** Its functionality is almost the same as the OSI transport layer. It enables peer entities on the network to carry on a conversation. Ex - TCP, UDP
3. **Internet :** The internet layer is the most important layer which holds the whole architecture together. It delivers the IP packets where they are supposed to be delivered.  Ex - IP, ICMP
4. **Link :** Decides which links such as serial lines or classic Ethernet must be used to meet the needs of the connectionless internet layer.


## Difference between OSI and TCP/IP Model :

![[diff_btw_osi_tcp_ip.png]]



## Difference between TCP and UDP :

1. **TCP** is a connection-oriented protocol, whereas **UDP** is a connectionless protocol. A key difference between TCP and UDP is *speed*, as TCP is comparetively slower than **UDP**. Overall UDP is a much faster, simpler and efficient protocol, however, retransmission of lost data packets is only possible with TCP.
2. TCP provides extensive error checking mechanism. It is because it provides flow control and acknowledgement of data. UDP has only the basic error checking mechanism using checksums.