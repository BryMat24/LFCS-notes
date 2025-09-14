## Kernel params

---

see kernel params

```
sysctl -a
```

change kernel params temporarily

```
sudo sysctl -w net.ipv6.conf.default.disable_ipv6 = 1
```

to make permanent, change the etc/sysctl.d, change the conf files

## Manage Virtual Machines

---

### KVM-QEMU (hypervisor, runs on top hardware - type 1)

QEMU = emulator/virtualizer (slow if pure emulation)
KVM = kernel module for hardware acceleration

### Steps (prebuilt disk image & os installed)

Install: libvirt, virt-install, virt-manager, qemu-img, qemu-info, libguestfs-tools

libvirt is the bridge between user space tools (virt-install, virt-manager) to the qemu

```
sudo apt install qemu-kvm libvirt-daemon-system virtinst virt-manager
sudo systemctl enable --now libvirtd
```

virsh commands

```
# create virtual machine through creating xml config file.
virsh define testmachine.xml

virsh list
virsh start <name>
virsh reboot <name> # graceful reboot
virsh destroy <name> # forceful shutdown
virsh reset <name> # force reset
virsh shutdown <name> # graceful shutdown
virsh autostart <name>
virsh dominfo <name>
virsh setvcpus <name> <number> --config
virsh setmaxmem TestMachine --size 2048MiB
virsh console <name>
virsh --connect ...

virsh shutdown <name> # delete the virtual machine
```

qemu-img

For managing VM disk image used by QEMU/KVM VM. Virtual disk is a file on the host that acts like a physical disk for virtual machines. Virtual disk contains the OS code.

```
qemu-img info <name-of-img>
qemu-img resize <name-of-img> 10G
```

virt-install

Tool to create the VM. A VM creation + installation tool, generate XML definition and starts the installation process. (boot from ISO)

```
virt-install --import --memory 512 --disk /var/lib/libvirt/images/ubuntu-22.04-minimal-cloudimg-amd64.img --os-variant ubuntu22.04 --name ubuntu1 --graphics none --vcpus 1
```

virt-customize

To setup pass root

```
sudo apt install libguestfs-tools
sudo virt-customize -a <disk> --root-password <password>
```

osquery

```
sudo apt install libosinfo-bin
osinfo-query os # see what operating system available/supported by virt-install
```

### Steps (empty disk)

ISO file is the installation media, it contains the installer for the OS, and installs the OS to the disk.

```
virt-install --memory 512 --location <iso-file> --os-variant ubuntu22.04 --name ubuntu1 --graphics none --vcpus 1
```
