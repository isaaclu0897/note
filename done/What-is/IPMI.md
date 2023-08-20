#what-is , #ipmi, #ipmitool

### What is IPMI

The **Intelligent Platform Management Interface (IPMI)** is a set of specifications that define a standardized method of managing and monitoring servers, especially those that are remote or difficult to access.

IPMI is a hardware solution independent of the server operating system, and is generally implemented through a **baseboard management controller ([[BMC]])**.

IPMI messages are transmitted over the **Intelligent Platform Management Bus ([IPMB](IPMB.md))**, a two-wire serial bus used for communication between Intelligent Platform Management Controllers (IPMCs) within the server. The IPMB typically employs the [[I2C]] (Inter-Integrated Circuit) protocol for implementation, a simple and low-speed serial communication protocol.

Simply put, IPMI is a specification **that provides features such as alerts, notifications, power control, and remote console access. IPMI is usually based on BMC and acts as an independent control system**, allowing administrators to monitor the status of servers.

---

### What can IPMI do?

IPMI can be a useful tool if you have **a large and complex server infrastructure that needs to be managed and monitored remotely**. However, if your environment is small or less complex, it may not be necessary.

Some of the key benefits of using IPMI include:

1. **System monitoring**: Enables administrators **to monitor the health and status of server hardware components**, including fans, power supplies, temperature sensors, and more.
2. **Remote management**: Allows administrators **to remotely manage and control servers, even when the operating system is unavailable or unresponsive**. This can include tasks such as power control, system resets, and accessing the server console remotely.
3. **Alerting and notifications**: Can **send alerts and notifications to administrators when hardware issues are detected**, such as overheating, fan failure, or power supply issues.

---

### How to Use IPMI?

The most popular IPMI tool is ipmitool. It is an open-source command-line utility used to manage and control system that support IPMI. It enables various IPMI operations through a command-line interface, such as remote power on/off, reboot, monitoring hardware status, and more.

#### Basic Commands

Here are some basic [[ipmitool]] commands that can be used to control the target system:

```bash
# Get System Info
ipmitool fru print

# Monitor Sensors
ipmitool sensor list

# Control Power
ipmitool power on
ipmitool power off
ipmitool power cycle

# View Event Log
ipmitool sel list
```

Using these commands, you can easily control and monitor servers or other operations remotely via IPMI.

