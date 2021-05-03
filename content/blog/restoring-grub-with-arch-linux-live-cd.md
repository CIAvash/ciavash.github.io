---
date: "2012-12-11T00:00:00Z"
title: Restoring GRUB with Arch linux live CD
categories: [Arch Linux]
tags: [Arch Linux, GRUB, Recovery]
aliases:
    - /blog/2012/12/11/restoring-grub-with-arch-linux-live-cd.html
---

I had Arch linux on my computer and needed Windows for gaming; Windows installs its own boot loader, so I had to re-install grub. The following is what I did to restore grub.

I suppose that you know what you're doing! For example you need to know in which partition linux is installed.

Boot Arch linux from live CD.

Create a directory for [chroot](https://wiki.archlinux.org/index.php/Change_Root) environment:

```bash
mkdir /mnt/root
```

Mount the root partition and other necessary device and file systems:

```bash
mount /dev/sda1 /mnt/root
cd /mnt/root
mount -o bind /dev dev/
mount -t proc proc proc/
mount -t sysfs sys sys/
```

It seems that on newer Arch releases(2012), you can use `arch-chroot /mnt/root` instead of the last 3 mount commands.

If you have a separate partition for boot, mount it:

```bash
mount /dev/[boot partition] boot/
```

Change the root:

```bash
chroot .
```

You can define another shell by adding it to the above command, like this:

```bash
chroot . /bin/bash
```

Generate grub.cfg file:

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

Install GRUB:

```bash
grub-install /dev/sda
```

Exit the chroot environment:
```bash
exit
```

Unmount filesystems and devices:

```bash
umount {dev,proc,sys,}
```

Unmount the root partition:

```bash
cd ..
umount root
```

And finally, you can reboot:

```bash
reboot
```