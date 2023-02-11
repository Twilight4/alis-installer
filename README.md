## Creating customized ISO and installing system
Before Installation - build the ISO
```
git clone https://github.com/Twilight4/alis-iso.git   # Download alis-iso repo
cd alis-iso/
vim alis.conf                                         # Edit configuration (network, intel drivers if you have and swap size)
./build-archlinux-with-alis.sh                        # Build the iso
#                                                     # Plug in the flash drive
sudo ventoy -i /dev/sdX                               # Check which device is the flash drive with fdisk -l or lsblk
cp ~/Alis-Out/select.iso /run/media/twilight/Ventoy/    # Create installation media using ventoy
```

Start the system with Arch Linux installation media
```
alis                                                  # Start installation using alis command
arch-chroot /mnt
bash <(curl -s https://raw.githubusercontent.com/Twilight4/arch-install/main/install-only-tweaks.sh)   # install my tweaks
bash <(curl -s https://raw.githubusercontent.com/Twilight4/arch-install/main/install-wifi-driver.sh)   # Install my wifi driver if you have to
exit
alis-reboot                                           # reboot using alis-reboot command
```

## Recovery
Boot from the latest <a href="https://www.archlinux.org/download/">original Arch Linux installation media</a>. After boot use the following commands to start the recovery, this will allow you to enter in the arch-chroot environment.

```
#                                # Start the system with latest Arch Linux installation media
iwctl --passphrase "[WIFI_KEY]" station [WIFI_INTERFACE] connect "[WIFI_ESSID]"            # Connect to WIFI network. _ip link show_ to know WIFI_INTERFACE
curl -sL https://git.io/JeaH6 | bash                                                       # Download official alis repo
./alis-recovery-asciinema.sh     # (Optional) Start asciinema video recording
vim alis-recovery.conf           # Edit configuration
./alis-recovery.sh               # Start recovery
./alis-recovery-reboot.sh        # Reboot the system
```

## SSH install and cloud-init

SSH install and cloud-init allows to install Arch Linux unattended and automated way in local virtual machines and cloud environments.

Build the cloud-init ISO, mount it in the VM along side the official Arch Linux installation media, start the VM and get its IP address.

```
$ ./alis-cloud-init-iso.sh
```

SSH to the VM.

```
$ ./alis-cloud-init-ssh.sh -i "${IP_ADDRESS}"
```

Or, start a unattended installation with the provided configuration.

```
$ ./alis-cloud-init-ssh.sh -i "${IP_ADDRESS}" -c "alis-config-efi-ext4-systemd.sh"
```
