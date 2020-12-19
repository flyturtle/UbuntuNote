# Ubuntu ver.EN
###### tags: `Ubuntu`
[toc]
>[time=Apr 24, 2018]
>CPU 
>>Intel^(r)^Core^(tm)^ i5-7400  3.0GHz*4[color=#000000]
>
>RAM 
>>8.00GB [color=#000000]
>
>GPU 
>Nvidia GeForce GTX 1050 [color=#000000]
>
>Disk
>>/dev/sda/ 
>>>WDC WD10EZEX-00MFCA0 (01.01A01)[color=#000000]
>>
>>/dev/sdb/
>>>TOSHIBA DT01ACA100 (MS2OA750)[color=#000000]
>
>os
>Ubnutu[color=#12ff12]
>17.10[time=Apr 24, 2018]
>18.04LTS[time=May 2, 2018]
>
>
>Triple boot win7,win10,ubuntu [time=May 31, 2018]
>Dual boot win10,ubuntu [time=Jun 6,2018]
>



## Boot/Kenrel
### Python change version

update-alternatives --config python

### install rtl8723bu
>os ubuntu 1810
>
>
>```lspci```check chipest information:
<pre><font color="#8AE234"><b>flyt1810@flyt1810</b></font>:<font color="#729FCF"><b>~/Documents/rtl8723bu-master</b></font>$ lspci
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
</pre>
>```lspci -vv -s 03:00.0``` show chipest more detail information:
<pre><font color="#8AE234"><b>flyt1810@flyt1810</b></font>:<font color="#729FCF"><b>~/Documents/rtl8723bu-master</b></font>$ lspci -vv -s 03:00.0
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
	Subsystem: ASUSTeK Computer Inc. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
	Control: I/O+ Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast &gt;TAbort- &lt;TAbort- &lt;MAbort- &gt;SERR- &lt;PERR- INTx-
	Latency: 0, Cache Line Size: 64 bytes
	Interrupt: pin A routed to IRQ 19
	Region 0: I/O ports at d000 [size=256]
	Region 2: Memory at f7104000 (64-bit, non-prefetchable) [size=4K]
	Region 4: Memory at f7100000 (64-bit, non-prefetchable) [size=16K]
	Capabilities: &lt;access denied&gt;
	Kernel driver in use: r8169
	Kernel modules: r8169
</pre>
>```sudo lshw -C network```
>
<pre> 
<font color="#8AE234"><b>flyt1810@flyt1810</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo lshw -C network
 *-network
       description: Wireless interface
       physical id: 2
       bus info: usb@1:10
       logical name: wlxf097e5008c07
       serial: f0:97:e5:00:8c:07
       capabilities: ethernet physical wireless
       configuration: broadcast=yes driver=rtl8723bu ip=192.168.1.104 multicast=yes wireless=IEEE 802.11bg
</pre>
### Install first
Recommended Partition [Link](https://askubuntu.com/questions/343268/how-to-use-manual-partitioning-during-installation)

### How to change mounting point?
https://askubuntu.com/questions/555280/how-to-change-mounting-point


:::info
get UUID
:::
```
sudo blkid
```
:::info
edit fstab
:::
```
sudo gedit /etc/fstab
```
:::info
add 
UUID="xxxx-xxxx"    /media/Radi ext4    defaults,user,auto  0   1
:::
reboot
```
sudo mount -a
```

cbe3c147-988a-4f3f-9a5a-7c4ce14b5ac8
### dd /make iso boot
>eg make iso boot
>
    sudo dd if=ubuntu-16.10-desktop-amd64.iso of=/dev/sdc bs=1M

check release & description:
```
lsb_release -a
```
    mkfs -t ext4 /dev/sdb1
### LVM
### Table disk of ubuntu
- Root
- Bin /executable programs are stored in 
- Sbin /executable programs are stored in 
- Etc /contains conf items like account
    - passwd
    - shadow
- Home /contains users home dir
- Lib /contains common libraries
- mnt /temp file systems are attached like cd rom or usb drive
- proc /virual file system stores kernel info
- tmp /contains temportaty
- usr /contains usr program and other data
    - bin 
    - man 
    - sbin
- var /variable data where system must be able to write buring operation
    - log
### Grub edit
:::info
180616
:::
[180616](//paste.ubuntu.com/p/VJrjfWD7h6/)
:::danger
No good for beginner.
:::
open and edit
```
$ sudo gedit /etc/default/grub
```


show in notepad
```
GRUB_DEFAULT=0
#GRUB_HIDDEN_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT_QUIET=true
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX="nomodeset access=v3"
GRUB_BACKGROUND='/home/flyturtle/Pictures/fgo.png'
```

and 

update
```
$ sudo update-grub
```

### Dual with Win10/Win7/macos
20180528
:::warning
Failed at WIN10X64_1511.ISO
:::
<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~/Downloads</b></font>$ sudo dd if=WIN10X64_1511.ISO of=/dev/sdb bs=16M
[sudo] password for flyturtle: 
236+1 records in
236+1 records out
3961208832 bytes (4.0 GB, 3.7 GiB) copied, 477.721 s, 8.3 MB/s
</pre>
WIN7_SP1X64.iso
<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~/Downloads</b></font>$ sudo dd if=WIN7_SP1X64.iso of=/dev/sdb bs=64M
[sudo] password for flyturtle: 
48+1 records in
48+1 records out
3239804928 bytes (3.2 GB, 3.0 GiB) copied, 265.576 s, 12.2 MB/s
</pre>


### Grub choose macos
:::warning
not tested
:::
https://www.maketecheasier.com/create-a-mac-entry-in-grub2/

http://paste.ubuntu.com/p/PMZ9nKTtKf/

### Boot repair
    The current session is in Legacy mode. Please reboot the computer, and use this software in an EFI session. 會啟用此功能 For example, use a live-USB of Boot-Repair-Disk-64bit (www.sourceforge.net/p/boot-repair-cd), after making sure your BIOS is set up to boot USB in EFI mode.
:::info
Paste from boot-repair at Wed, 30 May 2018 19:01:21 +0000
:::
http://paste.ubuntu.com/p/MDQB82xMRr/


Boot successfully repaired.

Please write on a paper the following URL:
http://paste.ubuntu.com/p/G8ZjHxQG87/


In case you still experience boot problem, indicate this URL to:
boot.repair@gmail.com or to your favorite support forum.

You can now reboot your computer.
Please do not forget to make your BIOS boot on sdb4/EFI/ubuntu/shimx64.efi file!

The boot files of [The OS now in use - Ubuntu 18.04 LTS] are far from the start of the disk. Your BIOS may not detect them. You may want to retry after creating a /boot/efi partition (FAT32, 100MB~250MB, start of the disk, boot flag). This can be performed via tools such as gParted. Then select this partition via the [Separate /boot/efi partition:] option of [Boot Repair].

If your computer reboots directly into Windows, try to change the boot order in your BIOS.
If your BIOS does not allow to change the boot order, change the default boot entry of the Windows bootloader.
For example you can boot into Windows, then type the following command in an admin command prompt:

https://askubuntu.com/questions/913397/how-to-change-ubuntu-install-from-legacy-to-uefi

    EFI detected. You may want to retry after activating the [Separate /boot/efi partition:] option.
Do you want to continue?

<pre><font color="#8AE234"><b>flyturtle_ubuntu_1804@flyturtle-ubuntu-1804-System-Product-Name</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo dpkg --configure -a
<font color="#8AE234"><b>flyturtle_ubuntu_1804@flyturtle-ubuntu-1804-System-Product-Name</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo apt-get install -fy
Reading package lists... Done
Building dependency tree       
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
<font color="#8AE234"><b>flyturtle_ubuntu_1804@flyturtle-ubuntu-1804-System-Product-Name</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo apt-get install -y lvm2
Reading package lists... Done
Building dependency tree       
Reading state information... Done
lvm2 is already the newest version (2.02.176-4.1ubuntu3).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
<font color="#8AE234"><b>flyturtle_ubuntu_1804@flyturtle-ubuntu-1804-System-Product-Name</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo apt-get purge -y grub*-common grub-common:i386 shim-signed
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Note, selecting &apos;grub-common&apos; for glob &apos;grub*-common&apos;
Note, selecting &apos;grub2-common&apos; for glob &apos;grub*-common&apos;
Package &apos;grub-common:i386&apos; is not installed, so not removed. Did you mean &apos;grub-common&apos;?
The following packages were automatically installed and are no longer required:
  mokutil shim
Use &apos;sudo apt autoremove&apos; to remove them.
The following packages will be REMOVED:
  grub-common* grub-efi-amd64* grub-efi-amd64-bin* grub-efi-amd64-signed*
  grub2-common* os-prober* shim-signed*
0 upgraded, 0 newly installed, 7 to remove and 0 not upgraded.
After this operation, 21.3 MB disk space will be freed.
(Reading database ... 173338 files and directories currently installed.)
Removing os-prober (1.74ubuntu1) ...
dpkg: warning: while removing os-prober, directory &apos;/var/lib/os-prober&apos; not empty so not removed
Removing shim-signed (1.34.9+13-0ubuntu2) ...
Removing grub-efi-amd64-signed (1.93+2.02-2ubuntu8) ...
Removing grub-efi-amd64 (2.02-2ubuntu8) ...
Removing grub-efi-amd64-bin (2.02-2ubuntu8) ...
Removing grub2-common (2.02-2ubuntu8) ...
Removing grub-common (2.02-2ubuntu8) ...
Processing triggers for install-info (6.5.0.dfsg.1-2) ...
Processing triggers for man-db (2.8.3-2) ...
(Reading database ... 172917 files and directories currently installed.)
Purging configuration files for grub-efi-amd64 (2.02-2ubuntu8) ...
Purging configuration files for shim-signed (1.34.9+13-0ubuntu2) ...
Purging configuration files for grub-common (2.02-2ubuntu8) ...
dpkg: warning: while removing grub-common, directory &apos;/etc/grub.d&apos; not empty so not removed
Processing triggers for ureadahead (0.100.0-20) ...
Processing triggers for systemd (237-3ubuntu10) ...
</pre>

---

http://paste.ubuntu.com/p/rHsWZmMcYt/
:::info
/dev/sda/ WDC WD10EZEX-00MFCA0 (01.01A01)
/dev/sdb/ TOSHIBA DT01ACA100 (MS2OA750)
:::


---
http://paste.ubuntu.com/p/zSp5y268Zj/
:::info
/dev/sda/ WDC WD10EZEX-00MFCA0 (01.01A01)
/dev/sdb/ TOSHIBA DT01ACA100 (MS2OA750)
:::

---
Finally
/dev/sda/ WDC WD10EZEX-00MFCA0 (01.01A01)
/dev/sdb/ TOSHIBA DT01ACA100 (MS2OA750)
 

## Driver
### gnome-shell
### ibus-chewing
    sudo apt install ibus-chewing
### Java
    sudo add-apt-repository ppa:webupd8team/java 
    
    sudo apt-get install oracle-java8-installer

    for dir in proc dev sys etc bin sbin var usr lib lib64 tmp; do
    mkdir /mnt/chrootdir/$dir && mount --bind /$dir /mnt/chrootdir/$dir
done

### atom
20180524
https://atom.io/
### UB4
20180522

Wifi hotspot: enable
[Driver](https://github.com/lwfinger/rtl8723bu)


    blacklist rtl8xxxu

in 

    sudo gedit /etc/modprobe.d/blacklist.conf

bluetooth: testing
```
[   14.176589] 8723bu: unknown parameter 'ips' ignored
[   14.177212] RTL871X: rtl8723bu v4.3.6.11_12942.20141204_BTCOEX20140507-4E40
[   14.177212] RTL871X: rtl8723bu BT-Coex version = BTCOEX20140507-4E40
[   14.230121] usbcore: registered new interface driver rtl8723bu
[   15.188750] rtl8723bu 1-6:1.2 wlxf097e5008c07: renamed from wlan0
[   15.217463] rtl8723bu 1-6:1.2 wlp0s20f0u6i2: renamed from wlan1

```
Under uefi ubuntu

<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-1804-LTS</b></font>:<font color="#729FCF"><b>~/Documents/UB4/rtl8723bu-master</b></font>$ sudo make
[sudo] password for flyturtle: 
make ARCH=x86_64 CROSS_COMPILE= -C /lib/modules/4.15.0-22-generic/build M=/home/flyturtle/Documents/UB4/rtl8723bu-master  modules
make[1]: Entering directory &apos;/usr/src/linux-headers-4.15.0-22-generic&apos;
Makefile:976: &quot;Cannot use CONFIG_STACK_VALIDATION=y, please install libelf-dev, libelf-devel or elfutils-libelf-devel&quot;
  Building modules, stage 2.
  MODPOST 1 modules
make[1]: Leaving directory &apos;/usr/src/linux-headers-4.15.0-22-generic&apos;
</pre>
<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-1804-LTS</b></font>:<font color="#729FCF"><b>~/Documents/UB4/rtl8723bu-master</b></font>$ sudo make
[sudo] password for flyturtle: 
make ARCH=x86_64 CROSS_COMPILE= -C /lib/modules/4.15.0-22-generic/build M=/home/flyturtle/Documents/UB4/rtl8723bu-master  modules
make[1]: Entering directory &apos;/usr/src/linux-headers-4.15.0-22-generic&apos;
Makefile:976: &quot;Cannot use CONFIG_STACK_VALIDATION=y, please install libelf-dev, libelf-devel or elfutils-libelf-devel&quot;
  Building modules, stage 2.
  MODPOST 1 modules
make[1]: Leaving directory &apos;/usr/src/linux-headers-4.15.0-22-generic&apos;
</pre>
#### Bluetooth Failed

<pre><font color="#EF2929"><b>Loading LTKs timed out for hci0</b></font>
</pre>

<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~</b></font>$ rfkill 
ID TYPE      DEVICE      SOFT      HARD
 0 wlan      phy0   unblocked unblocked
 1 wlan      phy1   unblocked unblocked
 2 bluetooth hci0   unblocked unblocked
</pre>

<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~</b></font>$ dmesg | grep tooth
[  424.080930] Blue<font color="#EF2929"><b>tooth</b></font>: Core ver 2.22
[  424.080970] Blue<font color="#EF2929"><b>tooth</b></font>: HCI device and connection manager initialized
[  424.080977] Blue<font color="#EF2929"><b>tooth</b></font>: HCI socket layer initialized
[  424.080981] Blue<font color="#EF2929"><b>tooth</b></font>: L2CAP socket layer initialized
[  424.080990] Blue<font color="#EF2929"><b>tooth</b></font>: SCO socket layer initialized
[  916.592426] Blue<font color="#EF2929"><b>tooth</b></font>: hci0: rtl: examining hci_ver=06 hci_rev=000b lmp_ver=06 lmp_subver=8723
[  916.592430] Blue<font color="#EF2929"><b>tooth</b></font>: hci0: rtl: loading rtl_bt/rtl8723b_fw.bin
[  916.598535] Blue<font color="#EF2929"><b>tooth</b></font>: hci0: rom_version status=0 version=1
[  916.749505] Blue<font color="#EF2929"><b>tooth</b></font>: BNEP (Ethernet Emulation) ver 1.3
[  916.749508] Blue<font color="#EF2929"><b>tooth</b></font>: BNEP filters: protocol multicast
[  916.749514] Blue<font color="#EF2929"><b>tooth</b></font>: BNEP socket layer initialized
[  917.164870] Blue<font color="#EF2929"><b>tooth</b></font>: RFCOMM TTY layer initialized
[  917.164884] Blue<font color="#EF2929"><b>tooth</b></font>: RFCOMM socket layer initialized
[  917.164893] Blue<font color="#EF2929"><b>tooth</b></font>: RFCOMM ver 1.11
[ 1594.134931] Blue<font color="#EF2929"><b>tooth</b></font>: hci0: last event is not cmd complete (0x0f)
</pre>
<pre>5月 25 07:11:14 flyturtle-Ubuntu-18-04LTS bluetoothd[8817]: <font color="#EF2929"><b>Unable to get Headset Voice gateway SDP record: Host is down</b></font></pre>

<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~</b></font>$ sudo hciconfig hci0 up
Can&apos;t init device hci0: Connection timed out (110)
</pre>
-  Bluetooth start failed
<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~</b></font>$ rfkill 
ID TYPE DEVICE      SOFT      HARD
 6 wlan phy6   unblocked unblocked
 7 wlan phy7   unblocked unblocked
</pre>
<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~</b></font>$ service bluetooth status 
● bluetooth.service - Bluetooth service
   Loaded: loaded (/lib/systemd/system/bluetooth.service; enabled; vendor preset
   Active: inactive (dead)
     Docs: man:bluetoothd(8)

[1]+  Stopped                 service bluetooth status
</pre>

<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~</b></font>$ dmesg |grep tooth
<font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~</b></font>$ dmesg |grep 8723
[   10.429209] <font color="#EF2929"><b>8723</b></font>bu: unknown parameter &apos;ips&apos; ignored
[   10.429850] RTL871X: rtl<font color="#EF2929"><b>8723</b></font>bu v4.3.6.11_12942.20141204_BTCOEX20140507-4E40
[   10.429851] RTL871X: rtl<font color="#EF2929"><b>8723</b></font>bu BT-Coex version = BTCOEX20140507-4E40
[   10.481136] usbcore: registered new interface driver rtl<font color="#EF2929"><b>8723</b></font>bu
[   11.249515] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlp0s20f0u6i2: renamed from wlan1
[   11.268760] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlxf097e5008c07: renamed from wlan0
[  896.938284] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlp0s20f0u6i2: renamed from wlan1
[  896.958553] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlxf097e5008c07: renamed from wlan0
[ 1104.790010] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlxf097e5008c07: renamed from wlan0
[ 1104.806799] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlp0s20f0u6i2: renamed from wlan1
[ 2512.224926] usbcore: deregistering interface driver rtl<font color="#EF2929"><b>8723</b></font>bu
[ 2542.409809] <font color="#EF2929"><b>8723</b></font>bu: unknown parameter &apos;ips&apos; ignored
[ 2542.410123] RTL871X: rtl<font color="#EF2929"><b>8723</b></font>bu v4.3.6.11_12942.20141204_BTCOEX20140507-4E40
[ 2542.410125] RTL871X: rtl<font color="#EF2929"><b>8723</b></font>bu BT-Coex version = BTCOEX20140507-4E40
[ 2542.474767] usbcore: registered new interface driver rtl<font color="#EF2929"><b>8723</b></font>bu
[ 2542.476357] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlxf097e5008c07: renamed from wlan0
[ 2542.495430] rtl<font color="#EF2929"><b>8723</b></font>bu 1-6:1.2 wlp0s20f0u6i2: renamed from wlan1
</pre>

[^first]:https://askubuntu.com/questions/466655/how-do-i-change-the-locale-of-wine-to-japanese-on-ubuntu-14-04
[^second]:https://code.google.com/archive/p/winelocale/wikis/AddLocalesToDebian.wiki


### gnome-bluetooth
[gnome-bluetooth-3.28.0](http://www.linuxfromscratch.org/blfs/view/systemd/gnome/gnome-bluetooth.html)
20180525
- GTK+-3.22.30 
- Wayland-1.15.0
- wayland-protocols-1.14
- [libxkbcommon-x11-dev_0.8.0-1_amd64.deb](https://ubuntu.pkgs.org/18.04/ubuntu-main-amd64/libxkbcommon-x11-dev_0.8.0-1_amd64.deb.html)
- xkbcommon
- doxygen
- wayland-egl
   - eglexternalplatform
- epoxy
 
### Wacom Draw
https://linuxwacom.github.io/
https://github.com/linuxwacom/xf86-input-wacom/wiki/Building-The-Driver

### Krita 
Install
```
sudo add-apt-repository ppa:kritalime/ppa
```
```
sudo apt update
```

```
sudo apt install krita
```
### Unity 3D
20180528
    sudo apt install gdebi
download .deb
gdebi [name].deb
wait
:::danger
use under win7 is best
:::
### Maya 
20180528
:::danger
use under win7 is best
:::
### woeusb 
20180529

:::info
WIN10X64_1511.ISO
:::
<pre><font color="#8AE234"><b>flyturtle@flyturtle-Ubuntu-18-04LTS</b></font>:<font color="#729FCF"><b>~/Documents/winiso</b></font>$ sudo woeusb --device WIN10X64_1511.ISO /dev/sdc
[sudo] password for flyturtle: 
WoeUSB v@@WOEUSB_VERSION@@

<font color="#4E9A06">Mounting source filesystem...</font>
<font color="#4E9A06">Wiping all existing partition table and filesystem signatures in /dev/sdc...</font>
/dev/sdc: 2 bytes were erased at offset 0x000001fe (dos): 55 aa
/dev/sdc: calling ioctl to re-read partition table: Success
<font color="#4E9A06">Ensure that /dev/sdc is really wiped...</font>
<font color="#4E9A06">Creating new partition table on /dev/sdc...</font>
<font color="#4E9A06">Creating target partition...</font>
<font color="#4E9A06">Making system realize that partition table has changed...</font>
Wait 3 seconds for block device nodes to populate...
mkfs.fat 4.1 (2017-01-24)
mkfs.fat: warning - lowercase labels might not work properly with DOS or Windows
<font color="#4E9A06">Mounting target filesystem...</font>
<font color="#C4A000">Applying workaround to prevent 64-bit systems with big primary memory from being unresponsive during copying files.</font>
<font color="#4E9A06">Copying files from source media...</font>
<font color="#4E9A06">Installing GRUB bootloader for legacy PC booting support...</font>
Installing for i386-pc platform.
Installation finished. No error reported.
<font color="#4E9A06">Installing custom GRUB config for legacy PC booting...</font>
<font color="#C4A000">Resetting workaround to prevent 64-bit systems with big primary memory from being unresponsive during copying files.</font>
<font color="#4E9A06">Unmounting and removing &quot;/media/woeusb_source_1527574165_2999&quot;...</font>
<font color="#4E9A06">Unmounting and removing &quot;/media/woeusb_target_1527574165_2999&quot;...</font>
<font color="#4E9A06">You may now safely detach the target device</font>
<font color="#4E9A06">Done :)</font>
<font color="#4E9A06">The target device should be bootable now</font>
</pre>


for dir in proc dev sys etc bin sbin var usr lib lib64 tmp; do mkdir /mnt/chrootdir/$dir && mount --bind / $dir /mnt/chrootdir/ $dir; done


### Networking Commands
whois domain
get whois for domain
ping host
pings host
dig domain
get DNS for domain
dig -x host
revserve lookup host
wget file
download file
wget -c file
continue stopped download
ssh user@host
connects as host
ssh -p port user@host
connects using port
ssh -d user@user
connects & binds port


### ffmpeg


```terminal=

```
ffmpeg -i 10_bit.mkv \
       -c:v libx265 -preset medium -x265-params crf=28 -pix_fmt yuv420p \
       -c:a copy \
       8_bit.mkv
       
       