#what-is , #ipmi, #ipmb , #protocol, #network , #communication 

### What is IPMB?

Intelligent Platform Management Bus(IPMB) is a two-wire serial bus used for communication between [[IPMI]] Controllers (IPMCs) within a server. IPMB typically employs the [[I2C]] (Inter-Integrated Circuit) protocol for implementation, which is a simple and low-speed serial communication protocol.

IPMB messages are organized into packets, **which consist of a header and a data payload**. The header contains information such as the packet type, source and destination addresses, and checksum. **The data payload contains the actual message being sent**, such as a request for sensor data or a command to power on the server.

In other words, we only need **to care about the data payload to decode the meaning of sending and receiving**.

### What is the IPMB packet format?

The IPMB protocol of the data payload and the meaning of each field are shown in the figure below:
![|340](../../../attachments/IPMB.png)
![|340](../../../attachments/IPMB-1.png)

### How to use IPMB

I believe it's best to look at actual examples. You can refer to [How to decode IPMI packet](../How%20to%20decode%20IPMI%20packet.md) for reference.

### Reference

> [NetFn and LUN](https://prayprogramer.wordpress.com/2015/06/02/ipmb%E9%80%9A%E8%A8%8A%E5%8D%94%E5%AE%9A%E7%AD%86%E8%A8%98/)