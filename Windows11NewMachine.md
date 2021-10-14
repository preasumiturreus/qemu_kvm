# Installation

Using virt-manager, created a new virtual machine by cloning a windows 10 machine configured with PCI passthrough of GPU and evdev keyboard and mouse. Removed windows 10 hard drive image. Created 150G qcow2 image for new machine.

Attached Windows11 iso and virtio-win iso so windows setup could install virtio drivers during installation to detect hard drive image.

First boot to uefi shell. Type 'exit' at shell to be taken to a 'BIOS' like menu. Use Boot selection option to boot Windows11 disk.

Installation process included several reboots. Finally booted to a windows desktop successfully. 

# Windows Configuration

Browsed virtio-win disk from Windows11. Attempted to install virtio-win-gt-x64.exe from virtio-win-0.1.208.
Received installer error code 2503, 2502.

In Device Manager, several devices have ! marks. To fix, right-click -> update driver. Select the virtio-win-0.1.208 folder, and windows will search and find the driver.

My system passes through an Nvidia GTX card; install nvidia driver using nvcleaninstall v1.10.0. Used only the driver, no other options. Resolution fixed automatically, manually configured refresh rate. 

# Saving system state

snapshot-create-as win11_passthroughUEFI --name win11_baseclean --description "from clean install, installed nvidia driver, some virtio-win driver, and startallback" --disk-only

The --disk-only option was required because without it the following error occurred: "error: Operation not supported: internal snapshots of a VM with pflash based firmware are not supported."

