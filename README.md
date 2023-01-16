## Creating customized ISO and installing system
```
sudo pacman -S archiso
git clone https://github.com/Twilight4/alis-iso.git   # Download alis repo
cd alis-iso
vim alis.conf                                         # Edit configuration
./build-archlinux-with-alis.sh                        # Build the iso
```

Create installation media using e.g. using balenaEtcher and start the system
```
chmod 755 /alis/*.sh
iwctl --passphrase "[WIFI_KEY]" station [WIFI_INTERFACE] connect "[WIFI_ESSID]"   # Connect to WIFI network. _ip link show_ to know WIFI_INTERFACE
alis                                                                              # Start installation using alis command
```

## Recovery
Boot from the latest <a href="https://www.archlinux.org/download/">original Arch Linux installation media</a>. After boot use the following commands to start the recovery, this will allow you to enter in the arch-chroot environment.

```
#                                # Start the system with latest Arch Linux installation media
iwctl --passphrase "[WIFI_KEY]" station [WIFI_INTERFACE] connect "[WIFI_ESSID]"            # Connect to WIFI network. _ip link show_ to know WIFI_INTERFACE
git clone https://github.com/Twilight4/alis-iso.git                                        # Download alis repo
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
