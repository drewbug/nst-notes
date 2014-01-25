Nook Simple Touch
=================

### CPU

`OMAP3621`

### Boot Sequence

`./devmem2 0x480022f0 b`

    /dev/mem opened.
    Memory mapped at address 0x40009000.
    Value at address 0x480022F0 (0x400092f0): 0x31

`ruby -e "puts 0x31.to_s(2).rjust(8, '0').reverse[0..4].reverse"`

    10001

According to page 3488 of the **OMAP36xx Technical Reference Manual** (*SWPU177B*), this means the boot sequence is:

    USB
    UART3
    MMC1
    MMC2

### (Equi-Length) uRamdisk Modifications

    mv uRamdisk uRamdisk-old
    tail -c +65 uRamdisk-old > uRamdisk.cpio.gz
    gzip -c -d uRamdisk.cpio.gz > uRamdisk.cpio && rm uRamdisk.cpio.gz
    
    ruby -e "File.open('uRamdisk.cpio', 'r+b') { |f| f.write f.read.sub('persist.service.adb.enable=0', 'persist.service.adb.enable=1').tap { f.rewind } }"
    
    gzip -c -9 uRamdisk.cpio > uRamdisk.cpio.gz && rm uRamdisk.cpio
    mkimage  -A ARM -O Linux -T RAMDisk -C gzip -n Image -d uRamdisk.cpio.gz uRamdisk-new && rm uRamdisk.cpio.gz
    chmod --reference=uRamdisk-old uRamdisk-new
    mv uRamdisk-new uRamdisk
