https://developer.nvidia.com/embedded/learn/jetson-orin-nano-devkit-user-guide/software_setup.html

https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit#write

https://developer.nvidia.com/embedded/jetpack
# ^ download image from here ASAP, it is 11GB zipped and can take 40-60min

```sh
# [dd method]

# ensure system has enough memory to download and unzip image ...

# insert sd card adapter & micro sd, ensure sd card adapter write protect switch is set to off

sudo dmesg | tail | awk '$3 == "sd" {print}'

#[ 7284.368382] sd 0:0:0:0: Attached scsi generic sg0 type 0
#[ 7284.971632] sd 0:0:0:0: [sda] 120879104 512-byte logical blocks: (61.9 GB/57.6 GiB)
#[ 7284.971979] sd 0:0:0:0: [sda] Write Protect is off
#[ 7284.971984] sd 0:0:0:0: [sda] Mode Sense: 2f 00 00 00
#[ 7284.972455] sd 0:0:0:0: [sda] Write cache: disabled, read cache: enabled, doesn't support DPO or FUA
#[ 7284.975622] sd 0:0:0:0: [sda] Attached SCSI removable disk

# attached card should NOT be mounted.
# dd works on block devices (bypassing filesystem) and should NOT be used on a mounted device.
# ensure card is unmounted via:
sudo umount /dev/sda # replace sda with where-ever device is attached, sdX

# check downloaded file name and /dev/sdX location
sudo /usr/bin/unzip -p ~/Downloads/jp61-orin-nano-sd-card-image.zip | sudo /bin/dd of=/dev/sda bs=1M status=progress
# ... ... 590282752 bytes (590 MB, 563 MiB) copied, 23 s, 25.7 MB/s ... ...

# check /dev/sdX location
sudo eject /dev/sda

# insert micro sd card into device, plug in power
# Note: my nano loaded 99% of the way and then failed to start the GUI the first time
# restarting and trying a 2nd time worked.
```
