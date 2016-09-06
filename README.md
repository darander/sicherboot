systemd Secure boot integration
===============================
sicher*boot automatically installs systemd-boot and kernels for it into the
[ESP][], signed with keys generated by it.

 [ESP]: https://en.wikipedia.org/wiki/EFI_System_partition

SECURITY
--------
The signing keys are stored unencrypted and only protected by the file system
permissions. Thus, you should make sure that the file system they are
stored (usually `/var`) in is encrypted.

Configuration
-------------
Kernel commandline can be placed in `/etc/kernel/cmdline`.

Limitations
-----------
* Only amd64/x64/x86_64 is supported for now
* Kernels and initramfs images must be named `/boot/vmlinuz-<ver>` and
  `/boot/initrd.img-<ver>`
* Only a single ESP is supported which must be mounted in /boot/efi
* Key generation is not done yet.


Integrating with your package management
----------------------------------------
You want to run:

* `sicherboot bootctl update`
  - whenever systemd is upgraded or installed
* `sicherboot install-kernel <ver>`
  - when the kernel is installed and the initramfs was built
* `sicherboot remove-kernel <ver>`
  - when the kernel shall be removed

As an example, kernel and initramfs contain integration with `/etc/kernel`
and initramfs-tools. Install one of the kernel postinst`.d` scripts - the dracut
one exists for dracut systems as a work around for dracut not supporting hooks.
