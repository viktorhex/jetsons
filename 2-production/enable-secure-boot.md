```sh
# NVIDIA Secure boot locks chain of trust down to hardware level (fuse)
# UEFI Secure boot is for general purpose OS security, but it seems like NVIDIA Secure boot is the way to go.

https://docs.nvidia.com/jetson/archives/r35.4.1/DeveloperGuide/text/SD/Security/SecureBoot.html

###########################################
############## DIDNT WORK #################
###########################################
# running ubuntu on host
# prereq says Linux for Tegra should be running on host but I only have normal Ubuntu 22.04
# I found some docs that show how to install specific Jetson components but I'm not sure that is the same as a full L4T running on host. I'll see how far I can get with this guide until I run into whatever I'm missing by not running L4T.

sudo apt-get install libftdi-dev
sudo apt install openssh-server

# install Jetpack Debian Packages on Host...
# is this a proper substitute for running L4T on host?
sudo apt-key adv --fetch-key http://repo.download.nvidia.com/jetson/jetson-ota-public.asc

# check ubuntu version with lsb_release -a

echo "deb http://repo.download.nvidia.com/jetson/x86_64/jammy r36.4 main" | sudo tee /etc/apt/sources.list.d/nvidia-jetson.list

## cuda
echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/ /" | sudo tee /etc/apt/sources.list.d/cuda.list

## nvida graphics sdk
echo "deb https://developer.download.nvidia.com/embedded/jetson-ota-public/ubuntu/ jammy main" | sudo tee /etc/apt/sources.list.d/nvidia-embedded.list

## add gpg keys
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/3bf863cc.pub
sudo apt-key adv --fetch-keys http://repo.download.nvidia.com/jetson/jetson-ota-public.asc

# check keys after adding:
# gpg --list-keys --no-default-keyring --keyring /etc/apt/trusted.gpg.d/cuda.gpg

sudo apt update

sudo apt-get install cuda-toolkit-12-2 cuda-cross-aarch64-12-2 nvsci libnvvpi3 vpi3-dev vpi3-cross-aarch64-l4t python3.9-vpi3 vpi3-samples vpi3-python-src nsight-systems-2023.4.3 nsight-graphics-for-embeddedlinux-2023.3.0.0
####################################################################
#############the above didnt work###################################
####################################################################

https://docs.nvidia.com/jetson/archives/r35.4.1/DeveloperGuide/text/SD/Security/SecureBoot.html#generate-a-pkc-key-pair

# Jetson Orin series targets support the PKC of RSA 3K, ECDSA P-256, and ECDSA P-521.

openssl ecparam -name secp521r1 -genkey -noout -out jetpackkey.pem
# The key file is used to burn fuses and sign boot files for Jetson devices.
# The security of your device depends on how securely you keep the key file.
### Tangential Project
# Secure generation and storage of keys with HSM
### 
# Instead of fusing the public key of a PKC key pair, only the hash of the public key is burned to the PublicKeyHash fuse field.

# How to access scripts required for secure boot on host os:
# install jetpack 6.x with nvidia sdk manager and then access scripts from within downloaded sdk files
# See:
# https://forums.developer.nvidia.com/t/orin-nano-devkit-tegrasign-v3-py-isnt-found/285274

# Next: Determine if it makes sense to enable UEFI Secureboot on top of Secure Boot
```
