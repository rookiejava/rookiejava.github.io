---
layout: post_page
title: Setting up Samsung Z3 for using Tizen .NET
---

These are the instructions to download and flash Tizen 4.0 platform image which is supporting Tizen .NET to your Samsung Z3.

### Step 1. Installing Tizen Development Tools

>**Requirements**: Tizen Development Tools only support the following Linux distribution versions.
>* Ubuntu 16.04/14.04/12.04
>* openSUSE 13.2/13.1/12.3/Leap 42.1
>* Fedora 23/22/21/20
>* CentOS 7/6
>* Debian 8/7

In order to download and install Tizen developement tools, you should add Tizen tools repository to the source list in advance.

`$ sudo vim /etc/apt/sources.list`

> For example:
> * In Ubuntu 16.04, append the following line to the source list:
>   * `deb [trusted=yes] http://download.tizen.org/tools/latest-release/Ubuntu_16.04/ /`
> * In Ubuntu 14.04, append the following line to the source list:
>   * `deb http://download.tizen.org/tools/latest-release/Ubuntu_14.04/ /`
>
> For more detail, please refer to [Developers Guide](https://source.tizen.org/documentation/developer-guide/getting-started-guide/installing-development-tools).

Now you can installing sdb and heimdall to flash Tizen platform binary to your Samsung Z3.

`$ sudo apt-get install sdb heimdall-flash`

### Step 2. Downloading Tizen 4.0 Platform Image

You shoud have the latest Tizen 4.0 Platform Image for mobile profile. You can download the latest version of Tizen 4.0 Platform Image (*.tar.gz) [here](http://download.tizen.org/snapshots/tizen/4.0-unified/latest/images/standard/mobile-wayland-armv7l-tm1/).

For example:

```
$ wget http://download.tizen.org/snapshots/tizen/4.0-unified/latest/images/standard/mobile-wayland-armv7l-tm1/tizen-4.0-unified_201803291_mobile-wayland-armv7l-tm1.tar.gz
```

> _Note that these are daily snapshots and at times may be unstable – try another binary if you face problems._

Then, extract the downloaded file (*.tar.gz) to any folder and go to the folder where you extract the zip file.

```
$ tar xvfz tizen-4.0-unified_20180329.1_mobile-wayland-armv7l-tm1.tar.gz
```

```
ramdisk.img
modules.img
rootfs.img
system-data.img
user.img
dzImage
ramdisk-recovery.img
```

### **Step 3. Flasging Tizen 4.0 Platform Image**

1. Connect Samsung Z3 to your linux

2. Set the target device into Download Mode

`$sdb root on && sdb shell "reboot download"`

Or, you can set the target device into download mode (without command line) as below :
* i.Turn the device off
* ii. Hold Volume Down + Home + Power buttons together
* iii. Press Volume Up to Continue

3. Flasing the image

```
$heimdall flash --KERNEL dzImage --MODULE modules.img --USER user.img --ROOTFS rootfs.img --SYSTEM-DATA system-data.img --RAMDISK1 ramdisk.img
```


When flashing is complete, the target will automatically reboot and you can detach the target device from your linux.

Enjoy Tizen .NET! 
