# Nokia N900 U-Boot/MultiBoot (NITDroid)

### Why not use U-Boot only?
- The CSSU has been recently taken down, and as a result it cannot be installed on factory reset units.
- Why does this matter? Because the CSSU is a requirement for the Wi-Fi, Bluetooth and some other core functions (which I forgot) to work properly.
- So as a result I wrote some scripts to bypass that and streamline the process of switching from Multiboot to U-Boot to boot either Android or Maemo Leste.
- If you have installed the CSSU prior to it being taken down you can use the files in this repo and the following guide https://talk.maemo.org/showthread.php?t=101338 but for all intents and purposes I will only be supporting the Multiboot method.
- I have also provided some U-Boot configs besides the Multiboot ones, if you have CSSU installed or want to boot a broken Android for some reason.
- Also I have also uploaded some QoL apps I use to make using the device easier.

Pre-requisites:
Install rootsh from the .deb provided in the repo

## Installation
This guide will assume you HAVE U-Boot installed if not, it should still be fine

a) Place the cloned folder to MyDocs/N900-UMBoot

b) Open XTerm and type:
> cd MyDocs/N900-UMBoot/boot/multiboot

> sudo gainroot

> sh multiboot-install.sh

> cd ../.. && dpkg -i NITDroid-Installer_0.2.8-8.deb

DO NOT LAUNCH THE INSTALLER

c) Close XTerm

d) Re-open XTerm and type the following commands:

> root

> cd /home/user/MyDocs/N900-UMBoot

> bzip2 -d N12_UMay.tar.bz2

> bzip2 -d N12_update_2.3.7.tar.bz2

> mkdir /and

> mount /home /and

> cd /and

> tar xvf /home/user/MyDocs/N900-UMBoot/nitdroid/N12_UMay.tar

> tar xvf /home/user/MyDocs/N900-UMBoot/nitdroid/N12_update_2.3.7.tar.bz2

> mkdir /etc/multiboot.d

> cp /home/user/MyDocs/N900-UMBoot/nitdroid/misc/init/init.nokia.rc /home

> cp /home/user/MyDocs/N900-UMBoot/nitdroid/uImage /home

> cp /home/user/MyDocs/N900-UMBoot/nitdroid/misc/init/init_subsys /home/system/maemo/bin

> dpkg -i /home/user/MyDocs/N900-UMBoot/nitdroid/nitdroid-installer_0.2.7_armel.deb

> sh /home/user/MyDocs/N900-UMBoot/boot/multiboot/multiboot-install.sh

> cp -r /home/user/MyDocs/N900-UMBoot/boot/multiboot/multiboot.d /etc

> cp /home/user/MyDocs/N900-UMBoot/boot/u-boot/bootmenu.d/50-*.item /etc/bootmenu.d

e) Now reboot and enjoy Android Gingerbread!

NOTE: If Android or multiboot don't work after reboot, try to launch the NITDroid-installer from the main application in order to fix possible issues or missing files/configuration.

## MUST-do on units with dead USB
a) Open XTerm and type:
> sudo gainroot

> cd ..

> cp MyDocs/N900-UMBoot/nitdroid/misc/dead-usb/init/init.nokia.rc init.nokia.rc 

NOTE: This breaks battery percentage and detection, but you can actually use the device. (The LED might still blink a very dim red due to Android thinking the battery level is low, but I added a workaround to dim it to the dimmest level. If it bothers you please tape the LED since I might never find a proper workaround)

## U-Boot Re-installation

a) Open XTerm and type:
> sudo gainroot

> sh MyDocs/N900-UMBoot/boot/u-boot/uboot-install.sh

b) Now reboot and U-Boot should be working.

## Multiboot Re-installation

a) Open XTerm and type:
> sudo gainroot

> sh MyDocs/N900-UMBoot/multiboot/multiboot-install.sh

b) Now reboot and Multiboot should be working. 

NOTE: In some cases you may reboot to U-Boot but if you select the Maemo entry it should go to Multiboot and fix itself, I'm guessing this is due to some kernel being mismatched?

## Install U-Boot Android entry (For CSSU users)

a) Open XTerm and type:
> sudo gainroot

> dpkg -i /home/user/MyDocs/N900-UMBoot/boot/u-boot/kernel-power/*.deb

> cp -r /home/user/MyDocs/N900-UMBoot/boot/u-boot/bootmenu.d/20-*.item /etc/bootmenu.d

> rm /etc/default/bootmenu.item

> ln -s /etc/bootmenu.d/20-*.item /etc/default/bootmenu.item

> u-boot-update-bootmenu

b) Now reboot and enjoy Android Gingerbread, also please note this will replace the omap kernel with the power kernel but the omap kernel will be reinstalled if you reinstall multiboot. (Which you shouldn't do if you have the CSSU installed)

## Post-install
a) Copy the "apk" folder from nitdroid/misc/apk in the cloned repo to the "MyDocs" folder, and then reboot to Gingerbread or transfer via USB, if your port isn't broken like mine is

a) Open Dev Tools, scroll down and tap on "Terminal Emulator"
> pm install /sdcard/apk/ZArchiver.apk

b) Now open ZArchiver and install any APK you want, I personally recommend installing Root Browser and FTPDroid

Credits:

https://t.me/linuxmobile_world

https://talk.maemo.org/showthread.php?t=101338

https://github.com/mattiacantalu/Nokia_N900_NITDroid

...and archive.org for archiving some .debs