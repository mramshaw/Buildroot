# Buildroot

Experiments with [Buildroot](http://www.buildroot.org/)

## What is Buildroot

From http://www.buildroot.org/

> Buildroot is a simple, efficient and easy-to-use tool to generate embedded Linux systems through cross-compilation

## Source Code

Pull the source code as follows:

    $ git clone git://git.busybox.net/buildroot

## Surprises

Unlike many linux projects, does not require root access or the use of `sudo`:

> No need to run as root, Buildroot is designed to be executed with normal user privileges.

And:

> Running as root is even strongly discouraged!

## Configuration

Offers many options:

Command|Requirements|Packages
-------|------------|--------
make menuconfig|ncurses|'ncurses-devel' or 'libncurses-dev' depending on distro
make nconfig|ncurses|'ncurses-devel' or 'libncurses-dev' depending on distro
make xconfig|Qt|Qt 4.8 or Qt 5.x
make gconfig|Gtk|gtk+-2.0, glib-2.0 and libglade-2.0

'ncurses' is the lightest framework so we will use that; on Ubuntu this requires 'libncurses5-dev'.

Both `make menuconfig` and `make nconfig` are now options; my preference is for `make nconfig`.

More importantly Buildroot offers a staggering number of predefined configurations:

```bash
$ ls -al ./configs/
total 808
drwxrwxr-x  2 owner owner 12288 May 25 12:11 .
drwxrwxr-x 16 owner owner  4096 May 25 12:14 ..
-rw-rw-r--  1 owner owner  1002 May 25 12:11 aarch64_efi_defconfig
 ...
<snip>
 ...
-rw-rw-r--  1 owner owner  1084 May 25 12:11 zynq_zed_defconfig
$
```

[The options include arm, bananapi, beaglebone, chromebook, raspberrypi and many others.]

#### Using a predefined configuration

This is a simple as <kbd>make savedefconfig</kbd>, for instance:

```bash
$ make beaglebone_defconfig
mkdir -p /home/owner/Documents/Linux/Buildroot/buildroot/output/build/buildroot-config/lxdialog
PKG_CONFIG_PATH="" make CC="/usr/bin/gcc" HOSTCC="/usr/bin/gcc" \
    obj=/home/owner/Documents/Linux/Buildroot/buildroot/output/build/buildroot-config -C support/kconfig -f Makefile.br conf
/usr/bin/gcc -D_GNU_SOURCE -DCURSES_LOC="<ncurses.h>" -DLOCALE  -I/home/owner/Documents/Linux/Buildroot/buildroot/output/build/buildroot-config -DCONFIG_=\"\"   /home/owner/Documents/Linux/Buildroot/buildroot/output/build/buildroot-config/conf.o /home/owner/Documents/Linux/Buildroot/buildroot/output/build/buildroot-config/zconf.tab.o  -o /home/owner/Documents/Linux/Buildroot/buildroot/output/build/buildroot-config/conf
#
# configuration written to /home/owner/Documents/Linux/Buildroot/buildroot/.config
#
$
```

The full configuration for a beaglebone has now been written to the default __.config__ file.

#### Building a predefined configuration

Now that our configuration options are defined, this is as simple as running <kbd>make</kbd>.

Of course, if you wish to keep a log of the build that can be done as follows:

    $ make 2>&1 | tee build.log

[Expect the initial build to take quite some time. Over a slow internet connection, it will ___really___ take some time.]

The built kernel image, bootloader image, and root filesystem image(s) will be in `output/images/`.

```bash
$ ls -alh output/images/
total 118M
drwxr-xr-x 2 owner owner 4.0K May 25 15:08 .
drwxrwxr-x 6 owner owner 4.0K May 25 15:08 ..
-rw-r--r-- 1 owner owner  36K May 25 15:08 am335x-boneblack.dtb
-rw-r--r-- 1 owner owner  35K May 25 15:08 am335x-bone.dtb
-rw-r--r-- 1 owner owner  35K May 25 15:08 am335x-bonegreen.dtb
-rw-r--r-- 1 owner owner  41K May 25 15:08 am335x-evm.dtb
-rw-r--r-- 1 owner owner  40K May 25 15:08 am335x-evmsk.dtb
-rw-r--r-- 1 owner owner  16M May 25 15:08 boot.vfat
-rw-r--r-- 1 owner owner  79K May 25 15:02 MLO
-rw-r--r-- 1 owner owner  60M May 25 15:08 rootfs.ext2
lrwxrwxrwx 1 owner owner   11 May 25 15:08 rootfs.ext4 -> rootfs.ext2
-rw-r--r-- 1 owner owner  15M May 25 15:08 rootfs.tar
-rw-r--r-- 1 owner owner  77M May 25 15:08 sdcard.img
-rw-r--r-- 1 owner owner 654K May 25 15:02 u-boot.img
-rw-r--r-- 1 owner owner  376 May 25 15:08 uEnv.txt
-rw-r--r-- 1 owner owner 5.3M May 25 15:08 zImage
$
```

## Reference

Various useful websites are listed below.

#### Home Page

The home page can be found here:

    http://www.buildroot.org/

#### Source Code Home Page

The source code can be found here:

    http://git.busybox.net/buildroot/

#### User Manual

The user manual can be found at:

    http://buildroot.org/downloads/manual/manual.html

## Credits

Buildroot Training:

    http://bootlin.com/doc/training/buildroot

[These documents change frequently so it is worth checking back often for the most up-to-date version.]

The source for these materials can be found at:

    http://github.com/bootlin/training-materials/

[Pull requests can be submitted here also.]
