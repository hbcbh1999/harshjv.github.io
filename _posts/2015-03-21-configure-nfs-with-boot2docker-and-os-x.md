---
layout: post
title: Configure NFS with boot2docker and OS X
description: Configure NFS with boot2docker and OS X
---

## Problem

When *boot2docker* is used with default *vboxfs* to mount shared folder `/Users`, it causes permission issues. For example, services do not have right to write to folders shared from host (OS X) to boot2docker.


## 1. Solution

This problem can be solved using **NFS** to share from host (OS X) to *boot2docker*.


## 2. OS X configuration

{% highlight bash %}
sudo echo "/Users -mapall=`whoami`:staff `boot2docker ip`" >> /etc/exports
{% endhighlight %}


## 3. Restart NFS server daemon

{% highlight bash %}
sudo nfsd stop && sudo nfsd start
{% endhighlight %}


## 4. Get into boot2docker

{% highlight bash %}
boot2docker ssh
{% endhighlight %}


## 5. boot2docker configuration

{% highlight bash %}
sudo echo "#! /bin/bash
sudo umount /Users
sudo /usr/local/etc/init.d/nfs-client start
sudo mount 192.168.59.3:/Users /Users -o rw,async,noatime,rsize=32768,wsize=32768,proto=tcp" > /var/lib/boot2docker/bootlocal.sh
{% endhighlight %}


## 6. Restart boot2docker or run the script

{% highlight bash %}
sh /var/lib/boot2docker/bootlocal.sh
{% endhighlight %}


## References

* [Comment](https://github.com/boot2docker/boot2docker/issues/581#issuecomment-74535277) by [paolomainardi](https://github.com/paolomainardi)
