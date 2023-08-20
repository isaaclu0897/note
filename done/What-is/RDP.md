#what-is , #windows , #rdp , #remote , #protocol 

### What is RDP (Remote Desktop Protocol)
Remote Desktop Protocol (RDP) is a proprietary protocol developed by Microsoft, which provides a user with a graphical interface to connect to another computer over a network connection.

### Why we need Remote Desktop on Windows
Why do we need RDP when we already have remote control in some scenarios?

#### The advantages of three RDP
* **Light and Fast**, In many cases, the bandwidth is small, and RDP can be very useful at that time.
* **Smart Resizing**, smart resizing of remote desktop windows.
* **Device and Driver Integration**, RDP effectively integrates hardware and driver resources, including disks, audio, input and hotkeys, activity signals, etc.

### Why do we need RDP in the real case
When we **use video redirection for [[iRMC]]**, we **often occur disconnections and freezes**, but the CPU resources of VM are not effectively utilized.

This is because video redirection for  iRMC consumes resources on the host, the host is busy enough, and it will be slower to continue to use host resources

So just use **RDP**, we can **resolve this huge performance** problem and improve user experience.

OKey, we also know RDP is very useful, but how to use it?
Find the content as [How to enable and use RDP on Windows](../How%20to%20enable%20and%20use%20RDP%20on%20Windows.md)

