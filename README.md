# Linuxium's scripts to create an Ubuntu LiveUSB


These scripts help create custom Ubuntu ISOs and LiveUSBs with the latest audio fixes for Intel platforms. Users will be able to test if their audio subsystem is supported in the latest Linux kernels (patches already queued for upstream integration and experimental ones) and report issues.

The scripts were initially based on the information documented on the following sites:

1. https://help.ubuntu.com/community/LiveCDCustomization (shared under a Creative Commons Attribution-ShareAlike 3.0 License available at https://help.ubuntu.com/community/License)
2. https://wiki.ubuntu.com/KernelTeam/GitKernelBuild (shared under a Creative Commons Attribution-ShareAlike 3.0 License available at https://help.ubuntu.com/community/License)

and then further developed by Linuxium (linuxium@linuxium.com.au) with contributions from Pierre-Louis Bossart.


The first script 'ubuntuliveusb.sh' downloads the latest experimental kernel with fixes for Intel audio platforms and then compiles it as Debian binary packages and creates a custom Ubuntu ISO. It is basically a wrapper for the following sub-scripts which are run in the following sequence: 

- ./1-create-development-chroot.sh - creates a development chroot environment based on an Ubuntu release ISO
- ./2-compile-development-chroot.sh - downloads the latest experimental kernel with fixes for Intel audio platforms and compiles it as Debian binary packages
- ./3-create-iso-chroot.sh - creates an ISO chroot environment based on an Ubuntu release ISO
- ./4-update-iso.sh - installs the custom kernel packages into the ISO chroot environment together with any additional packages which may be required
- ./5-make-iso.sh - creates the custom ISO from the ISO chroot environment

and uses the file 'include-chroot-variables.txt' which contains common variables required by all the scripts. The script is run by entering:

./ubuntuliveusb.sh

The actual kernel including how it is compiled is controlled by a further subset of scripts:

- 2a-start-compile-linux.source - controls the kernel and configs used in the compilation
- 2b-finish-compile-linux.source - tidies up afterward the compilation

Two additional standalone scripts are provided to help with any extra development requirements in the chroot environments. They are run by entering:

./enter-development-chroot.sh \<chroot environment\>

./exit-development-chroot.sh \<chroot environment\>


The second script 'ubuntumultiliveusb.sh' creates a bootable USB that can be used as a multiboot LiveUSB to boot the custom Ubuntu ISO and/or alternative Ubuntu ISOs selected via a multiboot menu. It is run by entering:

./ubuntumultiliveusb.sh /dev/\<usb device\>

and uses the file 'usb_partition/boot/grub/grub.cfg' to define the multiboot menu. ISOs can be added or removed by editing the script and menu configuration file. The installation of an ISO should be performed when actually running the ISO. The script includes a five second grace period allowing it to be interrupted as care should be taken to ensure the correct USB device is passed as the parameter in order to prevent accidental data corruption of any other USB device currently being used.


The scripts are provided as is in the hope that they are useful using the same Creative Commons license as the original Ubuntu wiki. The user is alerted to the fact that using experimental audio drivers and firmware may result in hardware damage for which there is no warranty or liability.

