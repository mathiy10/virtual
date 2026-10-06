# Experiment 5(a) — KVM Installation & Virtual Instances

## Universal Linux/KVM Commands

### 1. Check hardware virtualization support

```bash
egrep -c 'lm' /proc/cpuinfo
```

### 2. Display Linux kernel and system information

```bash
uname -a
lsmod | grep kvm
```

### 3. Install KVM, libvirt, Virt-Manager and required packages

```bash
sudo apt-get update
sudo apt-get install qemu-kvm libvirt-bin bridge-utils virt-manager qemu-system
```

### 4. Open the libvirt daemon configuration file

```bash
sudo nano /etc/libvirt/libvirtd.conf
```

### 5. Check non-commented entries in the libvirt daemon configuration

```bash
grep "[^#]" /etc/libvirt/libvirtd.conf
```

### 6. Check the libvirt configuration file

```bash
ls -l /etc/libvirt/libvirt.conf | grep "\*"
```

### 7. Check the libvirt daemon process

```bash
ps -ef | grep libvirtd
```

### 8. Open the libvirt interactive terminal

```bash
virsh
```

### 9. Display libvirt and QEMU version information

Run inside the `virsh` terminal:

```text
version
```

### 10. Display virtualization host/node information

Run inside the `virsh` terminal:

```text
nodeinfo
```

---

## Quick Command List

```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
uname -a
sudo apt-get update
sudo apt-get install qemu-kvm libvirt-bin bridge-utils virt-manager qemu-system
sudo nano /etc/libvirt/libvirtd.conf
grep "[^#]" /etc/libvirt/libvirtd.conf
ls -l /etc/libvirt/libvirt.conf | grep "\*"
ps -ef | grep libvirtd
virsh

5(a) KVM Installation - Minimal Commands cirros 0.5.1 x86 64 disk img

wget https://download.cirros-cloud.net/0.5.1/cirros-0.5.1-x86_64-disk.img

sudo apt install qemu-kvm libvirt-bin bridge-utils virt-manager qemu-system sudo systemctl restart libvirtd

virsh list

sudo virt-manager
```

Inside `virsh`:

```text
version
nodeinfo
```
download : wget https://download.cirros-cloud.net/0.5.1/cirros-0.5.1-x86_64-disk.img -O /var/lib/libvirt/images/cirros-disk.img

> **Note:** This Markdown contains only the command-line commands shown in Experiment 5(a) of the supplied document. GUI actions such as opening Virt-Manager, selecting options, downloading an image, and clicking **Forward/Finish** are intentionally excluded.
