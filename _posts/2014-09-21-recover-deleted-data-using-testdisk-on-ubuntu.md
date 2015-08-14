---
layout: post
title: Recover deleted data using TestDisk on Ubuntu
description: Recover deleted data using TestDisk on Ubuntu
keywords: "data recovery, testdisk, data recovery using testdisk, recover deleted data, recover deleted data using testdisk, ubuntu"
---

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

(From http://www.cgsecurity.org/wiki/TestDisk)

## Installation

To install **TestDisk** on Ubuntu,

{% highlight bash %}
apt-get install testdisk
{% endhighlight %}

You will need **root privileges** to install it, append `sudo` to invoke it as a root.

## Recovery

Open a terminal,

{% highlight bash %}
testdisk
{% endhighlight %}

Be sure to run it with **root privileges** by appending `sudo`.

![TestDisk: Select log file option](http://brightbucket.files.wordpress.com/2014/09/testdisk_1.png "Select log file option")

Select **Create** using arrow keys and press enter. This will create a log file for further inspection purpose.

![TestDisk: Select device](http://brightbucket.files.wordpress.com/2014/09/testdisk_3.png "Select device")

Now, select device you want to recover, and then **Proceed**.

![TestDisk: Select partition type](http://brightbucket.files.wordpress.com/2014/09/testdisk_4.png "Select partition type")

TestDisk will suggest you the partition table type of your drive, select it.

![TestDisk: Select advanced option](http://brightbucket.files.wordpress.com/2014/09/testdisk_5.png "Select advanced option")

Now, select **Advanced**. You will see a partition table for your device.

![TestDisk: Select partition](http://brightbucket.files.wordpress.com/2014/09/testdisk_6.png "Select partition")

Select a partition you want to recover, and navigate to **Undelete** form the bottom of the screen and select it.

![TestDisk: Select deleted data](http://brightbucket.files.wordpress.com/2014/09/testdisk_7.png "Select deleted data")

Found what you were looking for? Navigate to your deleted file or directory and press `c`.

![TestDisk: Select destination](http://brightbucket.files.wordpress.com/2014/09/testdisk_9.png "Select destination")

You will be asked to provide destination location where you want to save this deleted file, go there and press `c` to begin copy.

![TestDisk: Success](http://brightbucket.files.wordpress.com/2014/09/testdisk_10.png "Success")

If you want to recover all the data in a directory, press `a` to select all the files and then `Shift + c` to copy all the selected files to your destination directory, then provide destination directory, and press `c` to begin copy.

When you're done with recovery, press `q` to quit.
