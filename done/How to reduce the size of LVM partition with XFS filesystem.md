#how-to , #lvm, #xfs , #file-system, #centos , #linux 

**LVM, Logical Volume Manager**, is a storage management tool that can divide multiple hard disks into multiple logical volumes. The advantage of LVM is that it **allows you to dynamically adjust storage space without shutting down the system** or stopping services.

However, when you need to reduce the size of the LVM partition, if you **use the XFS file format, direct reduction is not feasible**. At this time, **you need to use xfsdump and xfsrestore for data backup and restoration**. In this article, we'll describe how to use these tools to reduce the size of LVM partitions, and what to look out for.

### Prerequisites

* CentOS Live CD
* another Disk for backup data

### How to reduce the size of LVM partition with XFS filesystem

1.  Boot Centos Live CD and enter resuce mode
2.  Backup filesystem using xfsdump
3.  Remove logical volumn then Create a smaller one
4.  Restore filesystem using xfsrestore
5. Remove unused space
6. Reboot you OS then Finish up!
7. But...wait if you use hyperv remember release vhdx


### Step by Step

#### Boot Centos Live CD and enter resuce mode

#### Backup filesystem using xfsdump

1. Active volumn group
    ```bash
    $ vgchange -ay
    $ lvdisplay # check logical volumn status available
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem.png)

2. Create mount folder
    ```bash
    $ mkdir /mnt/sysimage/root
    $ mkdir /mnt/sysimage/backup
    $ ls -al /mnt/sysimage/
    ```
3.  Mount filesystem and backup folder on it
    ```bash
    $ mount /dev/cl/root /mnt/sysimage/root    # mount filesytem
    $ mkfs.xfs /dev/sdb    # If your backup disk has not been formatted, please format it first
    $ mount /dev/sdb /mnt/sysimage/backup    # mount another disk for store filesystem backups
    $ df -h
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem-1.png)

4. Backup filesystem to backup folder using xfsfump
    dump label: root lv backup, media label: root-backup
    ```
    xfsdump -l 0 -L "root lv backup" -M "root-backup" -f /mnt/sysimage/backup/root.image /mnt/sysimage/root
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem-2.png)

#### Remove logical volumn then Create a smaller one

1. Umount root folder
    ```
    $ umount /mnt/sysimage/root/
    ```
2. Remove logical volumn
    ```
    $ lvremove /dev/cl/root
    ```
3. Check it works
    ```
    $ vgdisplay # check free size
    $ vgs # or use vgs command to check
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem-3.png)
4. Create smaller logical volumn
    ```
    $ lvcreate -L 150G -n root cl
    $ lvdisplay # check new lv
    $ mkfs.xfs /dev/cl/root
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem-4.png)

    
#### Restore filesystem using xfsrestore

1. Mount root folder
    ```bash
    $ mount /dev/cl/root /mnt/sysimage/root/
    ```
3. Restore filesystem to root folder
    ```bash
    $ xfsrestore -f /mnt/sysimage/backup/root.image /mnt/sysimage/root
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem-5.png)

#### Remove unused space

1. Check LVM status
    ```bash
    $ pvs
    $ vgs
    $ lvs
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem-6.png)
2. Remove unused vg and pv
    ```bash
    $ vgreduce cl /dev/sda3
    $ pvremove /dev/sda3
    ```
    ![|400](../../attachments/How%20to%20reduce%20the%20size%20of%20LVM%20partition%20with%20XFS%20filesystem-7.png)
    
#### Reboot you OS then Finish up!

#### But...wait if you use hyperv remember release vhdx

1. Remove unused partition using Gparted Live CD
2. Compact VHDX via HyperV
3. Shrink VHDX via HyperV
4. In my case, it does not work. So I reboot OS
5. Then compact it again. In fact I do not know how haha...


### Reference article

> [CentOS 7 XFS filesystem LVM](https://channing342.blogspot.com/2017/07/centos7-xfs-filesystem-lvm.html?m=1)
> [How to reduce the root of XFS filesystem](https://blog.51cto.com/linux2022/4755724)
> [How to reduce the root of XFS filesystem with LVM](https://www.dotblogs.com.tw/I_know_why_I_am/2020/10/01/042546)
> [The notice of LVM and reduce XFS](https://blog.csdn.net/mydriverc2/article/details/113794100)
> [How to reduce shrink the size of a lvm partition formatted with xfs filesystem](https://yallalabs.com/linux/how-to-reduce-shrink-the-size-of-a-lvm-partition-formatted-with-xfs-filesystem/)
> [LVM expand and reduce](https://dotblogs.com.tw/I_know_why_I_am/2020/09/30/235637)


