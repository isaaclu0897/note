#how-to , #ipmi , #ipmb , #wireshark , #protocol , #network , #communication , #decode

### How to decode IPMB?

[[IPMB]] stands for [[IPMI]] Bus, and it is a communication protocol used in IPMI to communicate with the baseboard management controller ([BMC](../todo/BMC)). To decode IPMB messages, you can use tools such as [ipmitool](../todo/ipmitool) in [[Linux]].

#### IPMB Packet Payload Example

When using ipmitool, you can send the NetFn = Chassis (0x00), CMD = 0x01 command by running the following command:

```bash
ipmitool raw <NetFn> <CMD>
ipmitool raw 0x00 0x01
 0x41 0x10 0x40 0x00
```

1. This will result in a Request IPMB packet payload data with the following bytes:

    ```
    Request IPMB packet payload data
    0x20 0x00 0xE0 0x20 0x10 0x01 0xCF
    ```
    * Byte 1: `0x20` - Response Slave Address
    * Byte 2: `0x00` - Response NetFn and LUN
    * Byte 3: `0xE0` - Response Checksum for Byte 1-2
    * Byte 4: `0x20` - Request Slave Address
    * Byte 5: `0x10` - Request NetFn and LUN
    * Byte 6: `0x01` - Command
    * Byte 7: `0xCF` - Response Checksum for Byte 6

2. The Response IPMB packet payload data will be as follows:

    ```
    Response IPMB packet payload data
    0x20 0x04 0xDC 0x20 0x10 0x01 0x00 0x21 0x01 0x40 0x00 0x6D
    ```

    * Byte 1: `0x20` - Request Slave Address
    * Byte 2: `0x04` - Request NetFn and LUN
    * Byte 3: `0xDC` - Request Checksum for Byte 1-2
    * Byte 4: `0x20` - Response Slave Address
    * Byte 5: `0x10` - Response NetFn and LUN
    * Byte 6: `0x01` - Command
    * Byte 7: `0x00` - Complete code
    * Byte 8-11: `0x21 0x01 0x40 0x00` - Response Data
    * Byte 12: `0x6D` - Response Checksum for Byte 4-11

> reference [NetFn and LUN](https://prayprogramer.wordpress.com/2015/06/02/ipmb%E9%80%9A%E8%A8%8A%E5%8D%94%E5%AE%9A%E7%AD%86%E8%A8%98/)
> ![|250](../../attachments/How%20to%20decode%20IPMI%20packet.png)
> ![|300](../../attachments/How%20to%20decode%20IPMI%20packet-1.png)

---

### How to calculate NetFn/LUN and checksum?

#### NetFn/LUN
To calculate the NetFn/LUN field, you need to combine the NetFn and LUN values. NetFn is a 6-bit value that can range from 0 to 63, while LUN is a 2-bit value that can range from 0 to 3. **To combine these values, you need to shift the NetFn value left by 2 bits and add it to the LUN value**.

For example, if you want to set the NetFn to `0x10` and the LUN to `0x01`, you would perform the following calculation:
```
NetFn = 0x10 << 2 = 0x40
LUN = 0x01
NetFn/LUN = NetFn + LUN = 0x41
```

#### checksum
To calculate the checksum for the IPMB packet payload, you need **to perform a "zero-checksum" on the relevant bytes**. For the request packet, this would be bytes 1 and 2 (the NetFn/LUN field), and for the response packet, this would be bytes 4 through 11 (the command, completion code, and data fields).

To perform a zero-checksum, **you need to add up all the bytes in the relevant range and take the two's complement of the result**. The two's complement is calculated by inverting all the bits and adding 1.

For example, to calculate the checksum for the request packet above:
```
Byte 1: 0x20
Byte 2: 0x04
Checksum: 2'sc((0x20 + 0x04) % 0x100) = 0xDC
```

Similarly, to calculate the checksum for the response packet:
```
Byte 4-11: 0x20 0x10 0x01 0x00 0x21 0x01 0x40 0x00
Checksum: 2'sc((0x20 + 0x10 + 0x01 + 0x00 + 0x21 + 0x01 + 0x40 + 0x00) % 0x100) = 0x6D

2'sc((0x20 + 0x10 + 0x01 + 0x00 + 0x21 + 0x01 + 0x40 + 0x00) % 0x100) = 0x6D
2'sc(0x93 % 0x100) = 0x6D
2'sc(0x93) = 0x6D
```

---

### How to find IPMB packet in WireShark?

Once you have identified the IPMI device's IP address, you can use [[WireShark]] to capture and analyze IPMB packets sent to and from the device.

1. Open WireShark and start capturing Ethernet traffic.
2. In the filter box, enter "ip.addr == [destination IP]" to filter packets by destination IP.
3. Send your IPMI command to the destination IP.
4. Look for the third-to-last packet, which should be the outgoing IPMB packet.
5. Look for the fourth-to-last packet, which should be the incoming response packet.

See the screenshot below for a visual guide:
![](../../attachments/How%20to%20decode%20IPMI%20packet-2.png)

Suppose we want to know how to control the IPMI commands of a set of software today. You can send the command to the machine first, and then use wireshark to check the meaning of his packet, that is very useful.

### Reference
> [Github ipmitool command](https://github.com/erik-smit/oohhh-what-does-this-ipmi-doooo-no-deedee-nooooo/blob/master/1-discovering/snippets/Computercheese/IPMI-Chassis%20Device%20Commands.txt)
> [IPMB Communication protocol note](https://prayprogramer.wordpress.com/2015/06/02/ipmb%E9%80%9A%E8%A8%8A%E5%8D%94%E5%AE%9A%E7%AD%86%E8%A8%98/)