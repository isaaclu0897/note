#how-to , #pxe , #dhcp , #tftp 
### Prerequisites

1. Check `<iPXE project>` is locate at `D:/RemoteInstall/Boot/ipxe` on Host
2. Prepare a HTTP Server for Linux ISO images and autoinstall files.
3. Prepare a DHCP Server to boot iPXE bootloader.

### How to setup iPXE

1. Create "settings.ipxe" for your environment.
2. Make the DHCP server chain to "settings.ipxe"
3. Mount the Linux ISO images and the autoinstall files from project to HTTP Server
4. PXE boot your SUT
5. Finish

### Step by Step

#### Create "settings.ipxe" for your environment.

1. Copy settings.ipxe.example from `<iPXE project>/settings.ipxe.example` to `<working folder>/settings.ipxe`
2. Edit "settings.ipxe" for your environment.
	```bash
	# Variables
	set tftp-url tftp://<your iPXE server IP>               # tftp root
	set tftp-boot-url ${tftp-url}/boot                      # tftp root/boot
	set tftp-ipxe-url ${tftp-url}/boot/ipxe                 # tftp root/boot/ipxe

	set http-url http://<your HTTP server IP>               # http root
	set http-images-file-url ${http-url}                    # http images file root
	set http-autoinstall-url ${http-url}/autoinstall        # http autoinstall root
	```
3. Make sure DHCP server is chain to "settings.ipxe".

#### Make the DHCP server chain to "settings.ipxe"

If you are using isc-dhcp-server on Linux, please refer to the following.

1. Edit your dhcp configuration.
    ```bash
    vim /etc/dhcp/dhcpd.conf
    ```
2. Insert the PXE settings below. Remember to modify `next-server <your iPXE server>`, according to your environment.
    ```bash
    option arch code 93 = unsigned integer 16;
    class "pxeclients" {
        match if substring (option vendor-class-identifier, 0, 9) = "PXEClient";
        next-server <your iPXE server IP>;
        if exists user-class and ( option user-class = "iPXE" ) {
            filename "/boot/ipxe/settings.ipxe";
        } elsif option arch = 00:07 or option arch = 00:09 {
            filename "/boot/ipxe/bin/ipxe.efi";
        } else {
            filename "/boot/ipxe/bin/ipxe.pxe";
        }
    }
    ```
3. Restrat the DHCP service.
    ```bash
    systemctl restart dhcpd.service
    ```

#### Mount the Linux ISO images and the autoinstall files from project to HTTP Server

1. Mount the autoinstall files from `<iPXE project>`
    ```bash
    mkdir -p <http server root>/autoinstall
    mount -t cifs //<your iPXE server IP>/reminst/Boot/ipxe/autoinstall <http server root>/autoinstall -o username=<username>,password=<password>
    ```
2. Mount the Linux ISO images
    ```bash
    mkdir -p <http server root>/rhel9_u3_em64t
    mount -o loop RHEL-9.3.0-20231025.65-x86_64-dvd1.iso <http server root>/rhel9_u3_em64t/
    ```
    
3. Your folder structure of http server looks like as below. The autoinstall files displayed in the folder are the OS we support.
    ```
    . <http repo root>
    ├── autoinstall
    │	├── efi
    │	│   ├── esxi6u7-v460-boot.cfg
    │	│   ├── esxi6u7-v470-boot.cfg
    │	│   ├── ...
    │	│   ├── sles15_sp5-ai.xml
    │	│   └── sles15_sp5-xen-ai.xml
    │	└── pcbios
    │		├── or7_u7-ks.cfg
    │		├── or7_u8-ks.cfg
    │		├── ...
    │		├── sles15_sp5-ai.xml
    │		└── sles15_sp5-xen-ai.xml
    │
    ├── or7_u7_em64t
    ├── or7_u8_em64t
    ├── ...
    ├── sles15_sp4_em64t
    ├── sles15_sp5_em64t
    └── vmware
        ├── esxi6u7-v460
        ├── esxi6u7-v470
        ├── ...
        ├── esxi8u1a
        └── esxi8u2
    ```

#### PXE boot your SUT

![](../../attachments/How%20to%20setup%20iPXE.png)

    
#### Finish