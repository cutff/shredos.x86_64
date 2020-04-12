# ShredOS 2020.02

ShredOS is a USB bootable small linux distribution with the sole purpose of securely erasing your
disks using the program [nwipe](https://github.com/martijnvanbrummelen/nwipe).

This version of Shredos includes the latest nwipe master, Smartmontools, a hexeditor [hexedit](https://linux.die.net/man/1/hexedit), that can be run in the second virtual terminal, ALT-F2, hdparm for wiping using the drives internal firmmware and loadkeys for setting the keyboard you are using. i.e. loadkeys uk, loadkeys fr etc.

ShredOS boots very quickly and depending upon the host system can boot in as little
as 2 seconds. Nwipe will then list the disks present on the host system. You can then
select the methods by which you want to securely erase the disk/s. Nwipe is able to
simultanuosly wipe multiple disks using a threaded software architecture.

For an upto date list of supported wipe methods see the [nwipe](https://github.com/martijnvanbrummelen/nwipe) page.
* Quick erase        - Fills the device with zeros, one round only.
* RCMP TSSIT OPS-II  - Royal Candian Mounted Police Technical Security Standard, OPS-II
* DoD Short          - The American Department of Defense 5220.22-M short 3 pass wipe. 1,2,& 7.
* DoD 5220.22M       - The American Department of Defense 5220.22-M full 7 pass wipe. 1-7
* Gutmann Wipe       - Peter Gutmann's method. (Secure Deletion of Data from Magnetic and Solid-State Memory)
* PRNG Stream        - Fills the device with a stream from the PRNG.
* Verify only        - This method only reads the device and checks that it is all zero.

Nwipe also includes the following pseudo random number generators:
* mersenne
* twister
* isaac

## Obtaining and running shredos the easy way !

You can of course compile shredos from source but that can take a long time and you can run into all sorts of problems if your not familiar with compiling an operating system. So if you just want to get started with using shredos anmd nwipe then just download the shredos image file and write it to a USB flash drive. Please note this will over write the existing contents of your USB flash drive.

Download the shredos image file from [here](https://github.com/PartialVolume/shredos.2020.02/releases/download/v2020.02.0.29rc.001/shredos.img.tar.gz)
```
Check it's not corrupt by running the following command and comparing with the checksum below:
$ sha1sum shredos.img.tar.gz
26dc684b18d41d22fedf01f642148ba648237a67  shredos.img.tar.gz

Unzip the image file
$ gunzip shredos.img.tar.gz
$ tar xvf shredos.img.tar

Write the .img file to your USB flash drive
dd if=shredos.img of=/dev/sdx (where sdx is the device name of your USB drive, this can be obtained from the results of sudo fdisk -l)

```

## Compiling ShredOS and burning to USB stick

The ShredOS system is built using buildroot.
The final system size is about 12MB but due to minimim fat32 partition size, the ending image is about
37MB and can be burnt onto a USB memory stick with a tool such as dd or Etcher.

You can build the image by doing:
```
$ git clone https://github.com/PartialVolume/shredos.2020.02.git
$ cd shredos
$ make shredos_defconfig
$ make
$ ls output/images/shredos*.img
$ cd output/images
$ dd if=shredos-20200412.img of=/dev/sdx (20200412 will be the day you compiled, sdx is the USB flash drive)
```

## shredos is based on buildroot

Buildroot is a simple, efficient and easy-to-use tool to generate embedded
Linux systems through cross-compilation.

The documentation can be found in docs/manual. You can generate a text
document with 'make manual-text' and read output/docs/manual/manual.text.
Online documentation can be found at http://buildroot.org/docs.html

To build and use the buildroot stuff, do the following:

1) run 'make menuconfig'
2) select the target architecture and the packages you wish to compile
3) run 'make'
4) wait while it compiles
5) find the kernel, bootloader, root filesystem, etc. in output/images

You do not need to be root to build or run buildroot.  Have fun!

Buildroot comes with a basic configuration for a number of boards. Run
'make list-defconfigs' to view the list of provided configurations.

Please feed suggestions, bug reports, insults, and bribes back to the
buildroot mailing list: buildroot@buildroot.org
You can also find us on #buildroot on Freenode IRC.

If you would like to contribute patches, please read
https://buildroot.org/manual.html#submitting-patches
