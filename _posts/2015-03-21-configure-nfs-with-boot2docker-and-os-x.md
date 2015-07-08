---
layout: post
title: Configure NFS with boot2docker and OS X
description: Configure NFS with boot2docker and OS X
keywords: "docker, boot2docker, nfs, permission, root permission, permission issue, write permission, configure, osx, os x, mac"
---

## Problem

When *boot2docker* is used with default *vboxfs* to mount shared folder `/Users`, it causes permission issues. For example, services do not have right to write to folders shared from host (OS X) to boot2docker.


## 1. Solution

This problem can be solved using **NFS** to share from host (OS X) to *boot2docker*.


## 2. OS X configuration

{% highlight bash %}
echo "$HOME -alldirs -mapall=$(whoami) -network 192.168.59.0 -mask 255.255.255.0" | sudo tee -a /etc/exports
{% endhighlight %}


## 3. Restart NFS server daemon

{% highlight bash %}
sudo nfsd restart
{% endhighlight %}


## 4. Configure boot2docker

{% highlight bash %}
boot2docker ssh "echo \"#! /bin/bash
sudo umount /Users && \
sudo /usr/local/etc/init.d/nfs-client start && \
sudo mkdir -p $HOME && sudo mount -t nfs -o noatime,soft,nolock,vers=3,udp,proto=udp,rsize=8192,wsize=8192,namlen=255,timeo=10,retrans=3,nfsvers=3 -v 192.168.59.3:$HOME $HOME\" | sudo tee /var/lib/boot2docker/bootlocal.sh && \
sudo chmod 755 /var/lib/boot2docker/bootlocal.sh"
{% endhighlight %}


## 6. Restart boot2docker or run the script

{% highlight bash %}
sh /var/lib/boot2docker/bootlocal.sh
{% endhighlight %}


## References

* [Comment](https://github.com/boot2docker/boot2docker/issues/581#issuecomment-74535277) by [paolomainardi](https://github.com/paolomainardi)
