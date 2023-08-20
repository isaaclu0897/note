
#how-to, #ipmi, #communication , #fujitsu


In the previous article, we introduced [How to decode IPMI packet](REPO/done/How%20to%20decode%20IPMI%20packet.md). However, today will explore the application of [[IPMI]] packets in a real server.

Through the previous content, you should already have the basic IPMI decoding ability, so we won't explain it in depth. In some cases, you need to have advanced control over the server. In this case, you need to understand the meaning of the packet.

Taking Fujitsu servers as an example, the following are the research results.

### How IPMI packets work on Fujitsu Server?

IPMI packets are used by Fujitsu servers to communicate with their server. **They consist of a NetFn, Command, and Data fields with Fujitsu-specific codes**.

Here are some examples of IPMI packets for reading and writing registers:

#### Read Register

* To read ConfBmcTftpUpdateServer
	* IPMI raw data > `0xB8 0xE0 0x80 0x28 0x00 0x01 0x00 0x69 0x19`
* To read Firmware Version[1]
	* IPMI raw data > `0xB8 0xE0 0x80 0x28 0x00 0x01 0x01 0x50 0x21`
	
#### Write Register

* To write `34` into ConfBmcTftpUpdateServer
	* IPMI raw data > `0xB8 0xE0 0x80 0x28 0x00 0x02 0x00 0x69 0x19 0x02 0x33 0x34`
* To write `4` into ConfBmcTftpUpdateServer
	* IPMI raw data > `0xB8 0xE0 0x80 0x28 0x00 0x02 0x00 0x69 0x19 0x01 0x34`
* To write `192.168.87.9453` into ConfBmcTftpUpdateServer
	* IPMI raw data > `0xB8 0xE0 0x80 0x28 0x00 0x02 0x00 0x69 0x19 0x0f 0x31 0x39 0x32 0x2e 0x31 0x36 0x38 0x2e 0x38 0x37 0x2e 0x39 0x34 0x35 0x33`

Finally, we can analyze the meaning of Fujitsu's IPMI packet:

* Byte 1: `0xB8` - NetFn
* Byte 2: `0xE0` - Command
* Byte 3: `0x80` - Data - Fujitsu code
* Byte 4: `0x28` - Data - Fujitsu code
* Byte 5: `0x02` - Data - Fujitsu command
* Byte 6: `0x00` - Data - Fujitsu register index
* Byte 7: `0x69` - Data - Fujitsu register lowwer byte
* Byte 8: `0x19` - Data - Fujitsu register higher byte
* Byte 9: `0x02` - Data - Fujitsu command length
* Byte 10: `0x33` - Data - Fujitsu data1
* Byte 11: `0x34` - Data - Fujitsu data2


### Write registers via .ini file using ipmiview Fujitsu provide

For more advanced IPMI control on Fujitsu Server, you can download from [Fujitsu official website](https://www.fujitsu.com/global/) and use the tools Fujitsu provide, and refer to the user manual of the tools.

To write a register value using an .ini file, first configure the .ini file with the desired values and then execute it. For example, to write the value `10.165.136.197` to register `1969`, you can use the following commands:
```
echo WriteConfigSpace = 0x1969, 0x00, "10.165.136.197" > i.ini
./IPMIVIEW64 -INI=i.ini
```

Or, using the IPMI raw data format:

```
IPMI raw data > `0xB8 0xE0 0x80 0x28 0x00 0x02 0x00 0x69 0x19 0x0f 0x31 0x39 0x32 0x2e 0x31 0x36 0x38 0x2e 0x38 0x37 0x2e 0x39 0x34 0x35 0x33`
```

In addition, I found a tool called Kalcheck, developed by Fujitsu seems to be very useful, but because it is used internally, we will not research it.

> Paper: Multi-aspect Full-system Server Model and Optimization Concept as a Simulation-based Approach (MFSMOS)
> Content: A special tool is called Kalcheck, developed by Fujitsu, which monitors the power and temperature values independently of the operating system. In particular, Kalcheck provides server-specific, internal system temperatures of the system-board, power supply unit, and each individual memory module. 
