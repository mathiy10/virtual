# EXP8 — OpenVSwitch and Linux Bridge

## Linux Bridge Commands

### 1. Check current network configuration

```bash
ip addr
```

### 2. Install Bridge Utilities

```bash
sudo apt install bridge-utils
```

### 3. Load the Linux bridge kernel module

```bash
sudo modprobe bridge
```

### 4. Load the br_netfilter kernel module

```bash
sudo modprobe br_netfilter
```

### 5. Edit the Netplan configuration

```bash
sudo nano /etc/netplan/<netplan-config>.yaml
```

Example universal Netplan structure:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    <INTERFACE>:
      dhcp4: no
  bridges:
    <BRIDGE_NAME>:
      interfaces: [<INTERFACE>]
      addresses: [<IP_ADDRESS>/<PREFIX>]
      gateway4: <GATEWAY>
      nameservers:
        addresses: [<DNS1>, <DNS2>]
```

### 6. Restart networking

```bash
sudo systemctl restart networking
```

### 7. Verify network interfaces and bridges

```bash
ip addr
```

```bash
ip link show type bridge
```

```bash
bridge link
```

### 8. Verify the routing table

```bash
route -n
```

### 9. Generate and apply Netplan configuration

```bash
sudo netplan generate
sudo netplan apply
```

---

## OpenVSwitch (OVS) Commands

### 10. Enter root/sudo shell

```bash
sudo -i
```

### 11. Create network namespaces

```bash
ip netns add <NAMESPACE_1>
ip netns add <NAMESPACE_2>
```

### 12. List network namespaces

```bash
ip netns list
```

### 13. Create virtual Ethernet pairs

```bash
ip link add <VETH_1> type veth peer name <VETH_2>
ip link add <VETH_3> type veth peer name <VETH_4>
```

### 14. List network interfaces

```bash
ip link
```

### 15. Assign virtual Ethernet ports to namespaces

```bash
ip link set <VETH_1> netns <NAMESPACE_1>
ip link set <VETH_3> netns <NAMESPACE_2>
```

### 16. Assign IP addresses to virtual Ethernet ports

```bash
ip netns exec <NAMESPACE_1> ifconfig <VETH_1> <IP_1> netmask <NETMASK> up
ip netns exec <NAMESPACE_2> ifconfig <VETH_3> <IP_2> netmask <NETMASK> up
```

### 17. Display the namespace interface configuration

```bash
ip netns exec <NAMESPACE_2> ifconfig
```

```bash
ip netns exec <NAMESPACE_1> ifconfig
```

### 18. Check routing tables inside namespaces

```bash
ip netns exec <NAMESPACE_1> route -n
ip netns exec <NAMESPACE_2> route -n
```

### 19. Install OpenVSwitch

```bash
sudo apt install openvswitch-switch openvswitch-common -y
```

### 20. Check OpenVSwitch version

```bash
ovs-vsctl --version
```

### 21. Check OpenVSwitch service status

```bash
sudo systemctl status openvswitch-switch
```

### 22. Start OpenVSwitch service if required

```bash
sudo systemctl start openvswitch-switch
```

### 23. Create an OVS bridge

```bash
ovs-vsctl add-br <BRIDGE_NAME>
```

### 24. Add virtual Ethernet ports to the OVS bridge

```bash
ovs-vsctl add-port <BRIDGE_NAME> <VETH_2>
ovs-vsctl add-port <BRIDGE_NAME> <VETH_4>
```

### 25. Display OVS configuration

```bash
ovs-vsctl show
```

### 26. Bring virtual Ethernet ports up

```bash
ifconfig <VETH_2> up
ifconfig <VETH_4> up
```

### 27. Configure an IP address for the OVS bridge/interface

```bash
ifconfig <BRIDGE_NAME> <BRIDGE_IP>/<PREFIX> up
```

### 28. Check the OVS bridge/interface status

```bash
ifconfig <BRIDGE_NAME>
```

### 29. Test connectivity between namespaces

```bash
ip netns exec <NAMESPACE_1> ping <NAMESPACE_2_IP>
```

### 30. Enable Spanning Tree Protocol (STP)

```bash
ovs-vsctl set bridge <BRIDGE_NAME> stp_enable=true
```

### 31. Display OVS database information

```bash
ovsdb-client dump
```

### 32. Check MAC addresses associated with the OVS bridge

```bash
ovs-appctl fdb/show <BRIDGE_NAME>
```

### 33. Check the MAC address of a namespace interface

```bash
ip netns exec <NAMESPACE_1> ifconfig <VETH_1>
```

```bash
ip netns exec <NAMESPACE_2> ifconfig <VETH_3>
```

---

## Quick Command List

### Linux Bridge

```bash
ip addr
sudo apt install bridge-utils
sudo modprobe bridge
sudo modprobe br_netfilter
sudo nano /etc/netplan/<netplan-config>.yaml
sudo systemctl restart networking
ip addr
ip link show type bridge
bridge link
route -n
sudo netplan generate
sudo netplan apply
```

### OpenVSwitch

```bash
sudo -i

ip netns add <NAMESPACE_1>
ip netns add <NAMESPACE_2>
ip netns list

ip link add <VETH_1> type veth peer name <VETH_2>
ip link add <VETH_3> type veth peer name <VETH_4>

ip link set <VETH_1> netns <NAMESPACE_1>
ip link set <VETH_3> netns <NAMESPACE_2>

ip netns exec <NAMESPACE_1> ifconfig <VETH_1> <IP_1> netmask <NETMASK> up
ip netns exec <NAMESPACE_2> ifconfig <VETH_3> <IP_2> netmask <NETMASK> up

sudo apt install openvswitch-switch openvswitch-common -y

ovs-vsctl --version
sudo systemctl status openvswitch-switch
sudo systemctl start openvswitch-switch

ovs-vsctl add-br <BRIDGE_NAME>
ovs-vsctl add-port <BRIDGE_NAME> <VETH_2>
ovs-vsctl add-port <BRIDGE_NAME> <VETH_4>
ovs-vsctl show

ifconfig <VETH_2> up
ifconfig <VETH_4> up
ifconfig <BRIDGE_NAME> <BRIDGE_IP>/<PREFIX> up
ifconfig <BRIDGE_NAME>

ip netns exec <NAMESPACE_1> ping <NAMESPACE_2_IP>

ovs-vsctl set bridge <BRIDGE_NAME> stp_enable=true
ovsdb-client dump
ovs-appctl fdb/show <BRIDGE_NAME>
```

> **Note:** Placeholders such as `<NAMESPACE_1>`, `<VETH_1>`, `<BRIDGE_NAME>`, `<IP_1>`, and `<ISO_PATH>` should be replaced with the values used in your own environment. The commands are extracted from the supplied Experiment 8 document and generalized without adding unrelated commands.
