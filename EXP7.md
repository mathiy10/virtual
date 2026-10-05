# Experiment 7(b) — VM Installation Using PowerShell

## Universal PowerShell Commands

### 1. Display available virtual switches

```powershell
Get-VMSwitch
```

### 2. Create a new virtual machine with a virtual hard disk

```powershell
New-VM -Name "<VM_NAME>" -NewVHDPath "<VHDX_PATH>" -NewVHDSizeBytes 30GB -Generation 2
```

### 3. Assign a virtual switch to the virtual machine

```powershell
Connect-VMNetworkAdapter -VMName "<VM_NAME>" -SwitchName "<SWITCH_NAME>"
```

### 4. Attach an Ubuntu ISO file to the virtual DVD drive

```powershell
Add-VMDvdDrive -VMName "<VM_NAME>" -Path "<ISO_PATH>"
```

Set the DVD drive as the first boot device:

```powershell
Set-VMFirmware -VMName "<VM_NAME>" -FirstBootDevice (Get-VMDvdDrive -VMName "<VM_NAME>")
```

### 5. Start the virtual machine

```powershell
Start-VM -Name "<VM_NAME>"
```

### 6. Check the status of the virtual machine

```powershell
Get-VM -Name "<VM_NAME>"
```

### 7. Stop the virtual machine

```powershell
Stop-VM -Name "<VM_NAME>"
```

---

## Quick Command List

```powershell
Get-VMSwitch

New-VM -Name "<VM_NAME>" -NewVHDPath "<VHDX_PATH>" -NewVHDSizeBytes 30GB -Generation 2

Connect-VMNetworkAdapter -VMName "<VM_NAME>" -SwitchName "<SWITCH_NAME>"

Add-VMDvdDrive -VMName "<VM_NAME>" -Path "<ISO_PATH>"

Set-VMFirmware -VMName "<VM_NAME>" -FirstBootDevice (Get-VMDvdDrive -VMName "<VM_NAME>")

Start-VM -Name "<VM_NAME>"

Get-VM -Name "<VM_NAME>"

Stop-VM -Name "<VM_NAME>"
```

> **Note:** `<VM_NAME>`, `<VHDX_PATH>`, `<SWITCH_NAME>`, and `<ISO_PATH>` are placeholders. Replace them with your own VM name, virtual disk path, virtual switch name, and ISO path.
