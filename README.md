wimboot: Windows Imaging Format bootloader for GRUB2
====================================================

This is an enhanced fork of [iPXE's wimboot](https://github.com/ipxe/wimboot/) with the pull-request from 
[Added support for loading initrd via the EFI LoadFile2 protocol](https://github.com/ipxe/wimboot/pull/49) by [a1ive](https://github.com/a1ive)

[`wimboot`][wimboot] is a boot loader for Windows Imaging Format
`.wim` files.  It enables you to boot into a [Windows PE
(WinPE)][winpe] deployment or recovery environment.

You can use `wimboot` with [iPXE][ipxe] to [boot Windows PE via
HTTP][howto].  With a Gigabit Ethernet network, a typical WinPE image
should download in just a few seconds.

Demo
----

This animation shows an HTTP network boot into the Windows 10
installer.  The total elapsed time from power on to reaching the
Windows installer screen is 17 seconds.

![Demo animation](doc/demo.gif)

Advantages
----------

### Speed

`wimboot` can download images at the full speed supported by your
network, since it can use HTTP rather than TFTP.

### Ease of use

`wimboot` works directly with `.wim` image files; there is no need to
wrap your `.wim` into an ISO or FAT filesystem image.

### BIOS/UEFI compatibility

`wimboot` allows you to use a single configuration and set of files to
boot under both BIOS and UEFI environments.

License
-------

`wimboot` is free software licensed under the [GNU General Public
License](LICENSE.txt).

Quickstart
----------

See https://ipxe.org/wimboot for instructions.


Grub Entry
----------

    menuentry "Wimboot" {
        linux /wimboot
        initrd newc:boot.wim:/src/boot.wim \
           newc:bcd:/src/bcd \
           newc:boot.sdi:/src/boot.sdi \
           newc:bootx64.efi:/src/bootx64.efi
    }

Extract/Copy the boot.wim, (bcd, boot.sdi, bootx64.efi...) from your installation source (i.e. Windows ISO)
and copy everything under grub's root-directory into a src/ subdirectory. Then add the entry above together
with the compiled wimboot(.x64_64 or .i386) file and try to boot.

[wimboot]: https://ipxe.org/wimboot
[ipxe]: https://ipxe.org
[winpe]: https://en.wikipedia.org/wiki/Windows_Preinstallation_Environment
[howto]: https://ipxe.org/howto/winpe
