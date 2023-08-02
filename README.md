## Creating Customized ISO and System Installation
### Before Installation - build the ISO
```bash
git clone https://github.com/Twilight4/alis-iso.git    # Download alis-iso repository
cd alis-iso/
vim alis.conf                                          # Edit configuration (network, intel drivers if you have and swap size)
./build-archlinux-with-alis.sh                         # Build the iso
#                                                      # Plug in the flash drive
umount /dev/sdX                                        # Check which device is the flash drive with fdisk -l or lsblk and Umount the flash drive
sudo ventoy -i -S -g /dev/sdX                          # Create installation media using ventoy
cp ~/Alis-Out/select.iso /run/media/$(whoami)/Ventoy/  # Copy the generated iso file to the installation media
```

### Start the system with Arch Linux installation media
```bash
#                                                     # Eject the usb thumb drive
alis                                                  # Start installation using alis command
arch-chroot /mnt
bash <(curl -s https://raw.githubusercontent.com/Twilight4/arch-setup/main/install-tweaks.sh)
#                                                     # Install security and performance tweaks
exit
alis-reboot                                           # Reboot using alis-reboot command
```
