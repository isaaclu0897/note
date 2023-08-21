#how-to , #windows , #pxe , #hyper-v , #vm

### Prerequisites
1. [DHCP](../todo/DHCP)
2. [PXE](../todo/PXE) Boot Server
3. [Hyper-V](../todo/Hyper-V) Server

### Step by step

1. Open HyperV Manager, Create New [Virtural Machine](../todo/Virtural Machine)
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV.png)
2. Give VM a Name
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-1.png)
3. Select Specify Gen, if you want to install UEFI, choose Gen2, or choose Gen1
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-2.png)
4. Enough Memory
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-3.png)
5. Select your Network, must be same with your DHCP and PXE Boot Server
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-4.png)
6. Enough Disk
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-5.png)
7. Choose 'Install from network', **Imporatnt! If you want to boot from PXE, need to choose it at here!** I don't why! Do not ask me! then you can click finish to complete setting.
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-6.png)
8. After Create the VM, you still have some setting must be setup, Right-Click and click settings...
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-7.png)
9. **Important Close Security Boot**
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-8.png)
10. Enough CPU
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-9.png)
11. Then you can boot your VM
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-10.png)
12. Waiting for PXE loading.
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-11.png)
13. Choose what you want to install form PXE menu
    ![|500](../../attachments/How%20to%20boot%20from%20PXE%20on%20HyperV-12.png)
14. Finish up!
