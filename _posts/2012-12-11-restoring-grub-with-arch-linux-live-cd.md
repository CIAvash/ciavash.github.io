---
layout: post
title: Restoring GRUB with Arch linux live CD
---

I had Arch linux on my computer and needed Windows for gaming; Windows installs its own boot loader, so I had to re-install grub. The following is what I did to restore grub.

I suppose that you know what you're doing! For example you need to know in which partition linux is installed.

Boot Arch linux from live CD.

Create a directory for [chroot](https://wiki.archlinux.org/index.php/Change_Root) environment:
{% highlight bash %}
mkdir /mnt/root
{% endhighlight %}

Mount the root partition and other necessary device and file systems:
{% highlight bash %}
mount /dev/sda1 /mnt/root
cd /mnt/root
mount -o bind /dev dev/
mount -t proc proc proc/
mount -t sysfs sys sys/
{% endhighlight %}

It seems that on newer Arch releases(2012), you can use `arch-chroot /mnt/root` instead of the last 3 mount commands.

If you have a separate partition for boot, mount it:
{% highlight bash %}
mount /dev/[boot partition] boot/
{% endhighlight %}

Change the root:
{% highlight bash %}
chroot .
{% endhighlight %}

You can define another shell by adding it to the above command, like this:
{% highlight bash %}
chroot . /bin/bash
{% endhighlight %}

Generate grub.cfg file:
{% highlight bash %}
grub-mkconfig -o /boot/grub/grub.cfg
{% endhighlight %}

Install GRUB:
{% highlight bash %}
grub-install /dev/sda
{% endhighlight %}

Exit the chroot environment:
{% highlight bash %}
exit
{% endhighlight %}

Unmount filesystems and devices:
{% highlight bash %}
umount {dev,proc,sys,}
{% endhighlight %}

Unmount the root partition:
{% highlight bash %}
cd ..
umount root
{% endhighlight %}

And finally, you can reboot:
{% highlight bash %}
reboot
{% endhighlight %}