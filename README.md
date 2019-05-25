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

[The options include arm, bananapi, beaglebone, chromebook, raspberrypi and other.]

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
