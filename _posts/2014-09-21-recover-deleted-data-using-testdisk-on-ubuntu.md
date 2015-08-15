---
layout: post
title: Recover deleted data using TestDisk on Ubuntu
description: Recover deleted data using TestDisk on Ubuntu
keywords: "data recovery, testdisk, data recovery using testdisk, recover deleted data, recover deleted data using testdisk, ubuntu"
---

## 1. Introduction

[TestDisk](http://www.cgsecurity.org/wiki/TestDisk) is an amazing data recovery tool available for Linux, Mac OS X and Windows under [GNU General Public License v2+](http://www.gnu.org/licenses/gpl.html).

TestDisk can -

* Fix partition table
* Recover deleted partition
* Recover FAT32 boot sector from its backup
* Rebuild FAT12/FAT16/FAT32 boot sector
* Fix FAT tables
* Rebuild NTFS boot sector
* Recover NTFS boot sector from its backup
* Fix MFT using MFT mirror
* Locate ext2/ext3/ext4 Backup SuperBlock
* Undelete files from FAT, exFAT, NTFS and ext2 filesystem
* Copy files from deleted FAT, exFAT, NTFS and ext2/ext3/ext4 partitions

> For more details, [http://www.cgsecurity.org/wiki/TestDisk](http://www.cgsecurity.org/wiki/TestDisk)

## 2. Installation

To install **TestDisk** on Ubuntu,

{% highlight bash %}
apt-get install testdisk
{% endhighlight %}

You will need **root privileges** to install it, append `sudo` to invoke it as a root.

## 3. Recovery

Open a terminal,

{% highlight bash %}
testdisk
{% endhighlight %}

Be sure to run it with **root privileges** by appending `sudo`.

![TestDisk: Select log file option](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-1.png "Select log file option")

Select **Create** using arrow keys and press enter. This will create a log file for further inspection purpose.

![TestDisk: Select device](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-3.png "Select device")

Now, select device you want to recover, and then **Proceed**.

![TestDisk: Select partition type](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-4.png "Select partition type")

TestDisk will suggest you the partition table type of your drive, select it.

![TestDisk: Select advanced option](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-5.png "Select advanced option")

Now, select **Advanced**. You will see a partition table for your device.

![TestDisk: Select partition](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-6.png "Select partition")

Select a partition you want to recover, and navigate to **Undelete** form the bottom of the screen and select it.

![TestDisk: Select deleted data](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-7.png "Select deleted data")

Found what you were looking for? Navigate to your deleted file or directory and press `c`.

![TestDisk: Select destination](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-9.png "Select destination")

You will be asked to provide destination location where you want to save this deleted file, go there and press `c` to begin copy.

![TestDisk: Success](/assets/images/posts/recover-deleted-data-using-testdisk-on-ubuntu/testdisk-10.png "Success")

If you want to recover all the data in a directory, press `a` to select all the files and then `Shift + c` to copy all the selected files to your destination directory, then provide destination directory, and press `c` to begin copy.

When you're done with recovery, press `q` to quit.
