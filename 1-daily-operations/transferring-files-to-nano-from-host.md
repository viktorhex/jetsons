```sh
# You can transfer your file SD card or USB device but if you would like to transfer your files directly, you can use “192.168.55.1” IP adres via ssh. You should connect the debug port via micro USB cable to your host PC. Than you can use “scp” with this IP address without internet connection.
# For example if your user name is nvidia for Jetson module;

scp <file_name> nvidia@192.168.55.1:/home/nvidia

# and also you connect to your Jetson module

ssh nvidia@192.168.55.1

# source: https://forums.developer.nvidia.com/t/transferring-files-from-pc-to-jetson-nano/172800
```
