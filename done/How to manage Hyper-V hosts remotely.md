#how-to, #hyper-v , #windows, #remote, #manage

As a administrator or developer, you might manage a lot of Hyper-V Servers. However, managing hosts independently is difficult.

So about how to remotely and centrally manage Hyper-V hosts is pretty important.

Next, Let's look at this.

### Prerequisites

* Hyper-V Server
* In my case
    * Hyper-V IP : 10.165.141.65
    * Hyper-V username : vincent.lee
    * Hyper-V password : <vincent.lee password in Hyper-V>

### How to manage Hyper-V hosts remotely

* Server Side
    * On the Hyper-V host to be managed, open a Windows PowerShell session as Administrator.
    * Create the necessary firewall rules for private network zones
    * To allow remote access on public zones, enable firewall rules for CredSSP and WinRM
    * You might need to update windows cumulative update ([CVE-2018-0886 → KB4103723](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB4103723))
* Client Side
    1. Install Hyper-V on your client (it could be your local computer)
    2. Add remote Hyper-V Server IP into your hosts file
    3. Configure the computer you'll use to manage the Hyper-V host
    4. Connect to Hyper-V Server Remotely
    5. Done

### Step by Step

#### Server Side (To do)

#### Client Side

1. Install Hyper-V on your client (it colud be your local computer)
    * Right click on the Windows button and select Apps and Features.
    * Select **Programs and Features** on the right under related settings.
    * Select **Turn Windows Features on or off**.
    * Select **Hyper-V** and click **OK**. (If you just want to manage Hyper-V hosts Remotely, you can install Management Tool only.)
      ![|500](../../attachments/How%20to%20manage%20Hyper-V%20hosts%20Remotely.png)
    * When the installation has completed you are prompted to restart your computer.

2. Add remote Hyper-V Server IP into your **hosts** file
    * Open **C:\Windows\System32\drivers\etc\hosts**
    * Add Hyper-V IP into localhost name resolution, and give it a name. (in my case, I use isaaclto as Hyper-V Server name)
    ![|500](../../attachments/How%20to%20manage%20Hyper-V%20hosts%20Remotely-1.png)

3. Configure the computer you'll use to manage the Hyper-V host
    * Open a Windows PowerShell session as Administrator.
    * Add all hosts into **TrustedHosts**
    ```powershell
    Set-Item WSMan:\localhost\Client\TrustedHosts -Value "*"
    ```
    * Enable delegate computer into **WSManCredSSP**
    ```powershell
    Enable-WSManCredSSP -Role client -DelegateComputer "isaaclto"
    ```
    * you might also need to configure the following group policy (**Allow delegating fresh credentials with NTLM-only server authentication**)
    ![|500](../../attachments/How%20to%20manage%20Hyper-V%20hosts%20Remotely-2.png)


4. Connect to Hyper-V Server Remotely
    * Right click on **Hyper-V Manager** at left-side panel, and click **Connect to Server...**
	![](../../attachments/How%20to%20manage%20Hyper-V%20hosts%20Remotely-3.png)
    * Type Hyper-V network place at **Another computer**
    * Check **Connect as another user**, click **Set User...**, type your **username** and **password** and click **remember me**, see as below.
	![|500](../../attachments/How%20to%20manage%20Hyper-V%20hosts%20Remotely-4.png)


5. Done
![|500](../../attachments/How%20to%20manage%20Hyper-V%20hosts%20Remotely-5.png)


### Reference article

> [Install Hyper-V on Windows 10](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)
> [Remotely manage Hyper-V hosts](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/manage/remotely-manage-hyper-v-hosts)
> https://www.youtube.com/watch?v=k_O2YOPcHtQ
> https://www.youtube.com/watch?v=LEZSgWL6SZY

#### Troubleshooting

> [Default credentials not being saved in Hyper-V Manager for a single VM](https://social.technet.microsoft.com/Forums/office/en-US/ab12a873-aaaa-43bb-a27d-ecec9cc6d6d4/default-credentials-not-being-saved-in-hyperv-manager-for-a-single-vm?forum=winserverhyperv)
> [Managing VM on a remote Hyper-V Server 2016 is show operation not supported](https://community.spiceworks.com/topic/2151820-managing-vm-s-on-a-remote-hyper-v-server-2016-operation-not-supported)
> see as below link
> [CVE-2018-0886](https://msrc.microsoft.com/update-guide/en-us/vulnerability/CVE-2018-0886)、[KB4103723](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB4103723)
> 

