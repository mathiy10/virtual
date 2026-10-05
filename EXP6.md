# EXP6

## 4. Access Shared Folder & Fix Permissions

Check mounted devices in `/media`. The shared folder appears as `sf_VMShared`:

### Terminal (VM1 & VM2)

```bash
ls /media
ls /media/sf_VMShared
```

### Permission Denied Fix

If regular users are denied access to `/media/sf_VMShared`, add your current user to the `vboxsf` system group and reboot:

### Terminal — Add User to vboxsf Group

```bash
sudo usermod -aG vboxsf $USER
sudo reboot
```

After rebooting, re-verify access:

### Terminal — Re-check Access

```bash
ls /media/sf_VMShared
```

### Fix Permissions with usermod (PDF Page 11)

Adding user to `vboxsf` group.

### Access Granted (PDF Page 11)

Viewing `22IT043.txt` inside `sf_VMShared`.

---

## 5. Transfer Files Between VMs

In **VM1**, copy a file into the shared folder:

### VM1 Terminal

```bash
cp VM1.txt /media/sf_VMShared/
```

Switch to **VM2**, and verify that the file is immediately available:

### VM2 Terminal

```bash
ls /media/sf_VMShared
cat /media/sf_VMShared/VM1.txt
```

Any change made in the shared folder from one VM is immediately accessible to the other VM.
