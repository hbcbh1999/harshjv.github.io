---
layout: post
title: Setup NFS with boot2docker and OS X
description: Setup NFS with boot2docker and OS X
categories:
  - docker
  - boot2docker
  - osx
  - open source
---

## Problem

When *boot2docker* is used with default *vboxfs* to mount shared folder `/Users`, it causes permission issues. For example, services do not have right to write to folders shared from host (OS X) to boot2docker.


### Solution

This problem can be solved using **NFS** to share from host (OS X) to *boot2docker*.


### OS X configuration

    sudo echo "/Users -mapall=`whoami`:staff `boot2docker ip`" >> /etc/exports


### Restart nfsd

    sudo nfsd stop && sudo nfsd start


### Get into boot2docker

    boot2docker ssh


### boot2docker configuration

	sudo echo "#! /bin/bash
	sudo umount /Users
	sudo /usr/local/etc/init.d/nfs-client start
	sudo mount 192.168.59.3:/Users /Users -o rw,async,noatime,rsize=32768,wsize=32768,proto=tcp" > /var/lib/boot2docker/bootlocal.sh


### Restart boot2docker or run the script

    sh /var/lib/boot2docker/bootlocal.sh
