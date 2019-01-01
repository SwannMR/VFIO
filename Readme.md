# Graphics Card Passthrough Method

This is my example of trying to get my Graphics Card passthrough into a Windows 7 VM. 

Details -

* Operating System: Arch Linux
* Motherboard: Asrock Z97 Extreme 4
* CPU: Intel(R) Core(TM) i7-4790K CPU @ 4.00GHz
* RAM: 16GB
* Graphics Card - https://www.techpowerup.com/vgabios/149015/sapphire-r9270-2048-130822

Graphics card does not support UEFI

## IOMMU Groups

```
IOMMU Group 0 00:00.0 Host bridge [0600]: Intel Corporation 4th Gen Core Processor DRAM Controller [8086:0c00] (rev 06)
IOMMU Group 10 00:1c.0 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 1 [8086:8c90] (rev d0)
IOMMU Group 11 00:1c.2 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 3 [8086:8c94] (rev d0)
IOMMU Group 12 00:1c.3 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 4 [8086:8c96] (rev d0)
IOMMU Group 13 00:1c.6 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 7 [8086:8c9c] (rev d0)
IOMMU Group 14 00:1d.0 USB controller [0c03]: Intel Corporation 9 Series Chipset Family USB EHCI Controller #1 [8086:8ca6]
IOMMU Group 15 00:1f.0 ISA bridge [0601]: Intel Corporation 9 Series Chipset Family Z97 LPC Controller [8086:8cc4]
IOMMU Group 15 00:1f.2 SATA controller [0106]: Intel Corporation 9 Series Chipset Family SATA Controller [AHCI Mode] [8086:8c82]
IOMMU Group 15 00:1f.3 SMBus [0c05]: Intel Corporation 9 Series Chipset Family SMBus Controller [8086:8ca2]
IOMMU Group 16 01:00.0 VGA compatible controller [0300]: Advanced Micro Devices, Inc. [AMD/ATI] Curacao PRO [Radeon R7 370 / R9 270/370 OEM] [1002:6811]
IOMMU Group 16 01:00.1 Audio device [0403]: Advanced Micro Devices, Inc. [AMD/ATI] Cape Verde/Pitcairn HDMI Audio [Radeon HD 7700/7800 Series] [1002:aab0]
IOMMU Group 17 02:00.0 Network controller [0280]: Qualcomm Atheros AR9287 Wireless Network Adapter (PCI-Express) [168c:002e] (rev 01)
IOMMU Group 18 04:00.0 Ethernet controller [0200]: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller [10ec:8168] (rev 11)
IOMMU Group 19 05:00.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 1 00:01.0 PCI bridge [0604]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller [8086:0c01] (rev 06)
IOMMU Group 20 06:01.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 21 06:03.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 22 06:05.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 23 06:07.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 24 08:00.0 SATA controller [0106]: ASMedia Technology Inc. ASM1062 Serial ATA Controller [1b21:0612] (rev 02)
IOMMU Group 25 0a:00.0 SATA controller [0106]: ASMedia Technology Inc. ASM1062 Serial ATA Controller [1b21:0612] (rev 02)
IOMMU Group 26 0b:00.0 USB controller [0c03]: ASMedia Technology Inc. ASM1042A USB 3.0 Host Controller [1b21:1142]
IOMMU Group 2 00:01.1 PCI bridge [0604]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x8 Controller [8086:0c05] (rev 06)
IOMMU Group 3 00:02.0 VGA compatible controller [0300]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor Integrated Graphics Controller [8086:0412] (rev 06)
IOMMU Group 4 00:03.0 Audio device [0403]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller [8086:0c0c] (rev 06)
IOMMU Group 5 00:14.0 USB controller [0c03]: Intel Corporation 9 Series Chipset Family USB xHCI Controller [8086:8cb1]
IOMMU Group 6 00:16.0 Communication controller [0780]: Intel Corporation 9 Series Chipset Family ME Interface #1 [8086:8cba]
IOMMU Group 7 00:19.0 Ethernet controller [0200]: Intel Corporation Ethernet Connection (2) I218-V [8086:15a1]
IOMMU Group 8 00:1a.0 USB controller [0c03]: Intel Corporation 9 Series Chipset Family USB EHCI Controller #2 [8086:8cad]
IOMMU Group 9 00:1b.0 Audio device [0403]: Intel Corporation 9 Series Chipset Family HD Audio Controller [8086:8ca0]
```

## Configuration

Add 

/etc/libvirt/qemu.conf
```
nvram = [
	"/usr/share/ovmf/x64/OVMF_CODE.fd:/usr/share/ovmf/x64/OVMF_VARS.fd"
]
```



With archlinux-lts kernel (bad)

```
IOMMU Group 0 00:00.0 Host bridge [0600]: Intel Corporation 4th Gen Core Processor DRAM Controller [8086:0c00] (rev 06)
IOMMU Group 10 00:1c.2 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 3 [8086:8c94] (rev d0)
IOMMU Group 11 00:1c.3 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 4 [8086:8c96] (rev d0)
IOMMU Group 12 00:1c.6 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 7 [8086:8c9c] (rev d0)
IOMMU Group 13 00:1d.0 USB controller [0c03]: Intel Corporation 9 Series Chipset Family USB EHCI Controller #1 [8086:8ca6]
IOMMU Group 14 00:1f.0 ISA bridge [0601]: Intel Corporation 9 Series Chipset Family Z97 LPC Controller [8086:8cc4]
IOMMU Group 14 00:1f.2 SATA controller [0106]: Intel Corporation 9 Series Chipset Family SATA Controller [AHCI Mode] [8086:8c82]
IOMMU Group 14 00:1f.3 SMBus [0c05]: Intel Corporation 9 Series Chipset Family SMBus Controller [8086:8ca2]
IOMMU Group 15 04:00.0 Ethernet controller [0200]: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller [10ec:8168] (rev 11)
IOMMU Group 16 05:00.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 17 06:01.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 18 06:03.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 18 08:00.0 SATA controller [0106]: ASMedia Technology Inc. ASM1062 Serial ATA Controller [1b21:0612] (rev 02)
IOMMU Group 19 06:05.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 1 00:01.0 PCI bridge [0604]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller [8086:0c01] (rev 06)
IOMMU Group 1 00:01.1 PCI bridge [0604]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x8 Controller [8086:0c05] (rev 06)
IOMMU Group 1 01:00.0 VGA compatible controller [0300]: Advanced Micro Devices, Inc. [AMD/ATI] Curacao PRO [Radeon R7 370 / R9 270/370 OEM] [1002:6811]
IOMMU Group 1 01:00.1 Audio device [0403]: Advanced Micro Devices, Inc. [AMD/ATI] Cape Verde/Pitcairn HDMI Audio [Radeon HD 7700/7800 Series] [1002:aab0]
IOMMU Group 1 02:00.0 Network controller [0280]: Qualcomm Atheros AR9287 Wireless Network Adapter (PCI-Express) [168c:002e] (rev 01)
IOMMU Group 20 06:07.0 PCI bridge [0604]: ASMedia Technology Inc. Device [1b21:1184]
IOMMU Group 20 0a:00.0 SATA controller [0106]: ASMedia Technology Inc. ASM1062 Serial ATA Controller [1b21:0612] (rev 02)
IOMMU Group 21 0b:00.0 USB controller [0c03]: ASMedia Technology Inc. ASM1042A USB 3.0 Host Controller [1b21:1142]
IOMMU Group 2 00:02.0 VGA compatible controller [0300]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor Integrated Graphics Controller [8086:0412] (rev 06)
IOMMU Group 3 00:03.0 Audio device [0403]: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller [8086:0c0c] (rev 06)
IOMMU Group 4 00:14.0 USB controller [0c03]: Intel Corporation 9 Series Chipset Family USB xHCI Controller [8086:8cb1]
IOMMU Group 5 00:16.0 Communication controller [0780]: Intel Corporation 9 Series Chipset Family ME Interface #1 [8086:8cba]
IOMMU Group 6 00:19.0 Ethernet controller [0200]: Intel Corporation Ethernet Connection (2) I218-V [8086:15a1]
IOMMU Group 7 00:1a.0 USB controller [0c03]: Intel Corporation 9 Series Chipset Family USB EHCI Controller #2 [8086:8cad]
IOMMU Group 8 00:1b.0 Audio device [0403]: Intel Corporation 9 Series Chipset Family HD Audio Controller [8086:8ca0]
IOMMU Group 9 00:1c.0 PCI bridge [0604]: Intel Corporation 9 Series Chipset Family PCI Express Root Port 1 [8086:8c90] (rev d0)
[root@super-archlinux pci-passthrough]# 
[root@super-archlinux pci-passthrough]# 
[root@super-archlinux pci-passthrough]# 
[root@super-archlinux pci-passthrough]# 
[root@super-archlinux pci-passthrough]# 
[root@super-archlinux pci-passthrough]# 
(reverse-i-search)`start': virsh ^Cart ubuntu_18-04
[root@super-archlinux pci-passthrough]# 
[root@super-archlinux pci-passthrough]# 
[root@super-archlinux pci-passthrough]# uname -a
Linux super-archlinux 4.14.56-1-lts #1 SMP Tue Jul 17 20:11:42 CEST 2018 x86_64 GNU/Linux
```

Receive the following error when starting win10 on virsh

```
[root@super-archlinux pci-passthrough]# virsh start win10
error: Failed to start domain win10
error: internal error: process exited while connecting to monitor: 2018-08-09T13:57:39.788375Z qemu-system-x86_64: -device vfio-pci,host=01:00.0,id=hostdev0,bus=pci.0,addr=0xa: vfio error: 0000:01:00.0: group 1 is not viable
Please ensure all devices within the iommu_group are bound to their vfio bus driver
```

## Audio

VM Off

```
➜  ~ sudo lspci -vs 01:00.1 | grep 'MSI:'
	Capabilities: [a0] MSI: Enable- Count=1/1 Maskable- 64bit+
```


VM started

```
➜  ~ sudo lspci -vs 01:00.1 | grep 'MSI:'
	Capabilities: [a0] MSI: Enable- Count=1/1 Maskable- 64bit+
```


This means my windows 10 install does not have MSI enabled

Might be work around

> one last thing is the audio, i spent far too much time trying to figure out the stuttering choppy sound that i see around the web in relation to vfio. for me, the solution was using pulseaudio with pulseeffects from the aur. > pulseeffects is an effects program that will handle the correct levels and create an audio buffer, mixing everything how i like. then, go into advance speaker properties in windows 10 and set the format to 44100Hz. this solved it for me


Command to run winows manually

# Installing

```
qemu-system-x86_64 -bios /usr/share/ovmf/ovmf_x64.bin -enable-kvm -cpu host -smp 4 -m 2048 -cdrom ~/Downloads/Win10_English_x64.iso -net nic,model=virtio -net user -drive file=~/vm/win10.hd.img.raw,format=raw,if=virtio -vga qxl -drive file=~/Downloads/virtio-win-0.1.105.iso,index=1,media=cdrom
```

# Running

```
qemu-system-x86_64 -bios /usr/share/ovmf/ovmf_x64.bin -enable-kvm -cpu host -smp 4 -m 4096 -net nic,model=virtio -net user -drive file=~/vm/win10.hd.img.raw,format=raw,if=virtio -vga qxl -usbdevice tablet -rtc base=utc
```