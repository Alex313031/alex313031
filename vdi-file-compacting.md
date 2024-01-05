Source: [StackOverflow](http://superuser.com/questions/529149/how-to-compact-virtualboxs-vdi-file-size)

## 1. Run `defrag` in the guest (Windows only)
## 2. Nullify free space:

**With a Linux Guest run this:**

```{.bash}
sudo dd if=/dev/zero | pv | sudo dd of=/bigemptyfile bs=4096k
sudo rm -rf /bigemptyfile
```

or

```{.bash}
telinit 1
mount -o remount,ro /dev/sda1
zerofree -v /dev/sda1
```

**With a Windows Guest, download `SDelete` from `SysInternals` and run this:**

```
sdelete.exe c: -z
```

(replace `C:` with the drive letter of the VDI)

## 3. Shutdown the guest VM
## 4. Now run VBoxManage's `modifyhd` command with the `--compact` option:

**With a Linux Host run this:**

```{.bash}
vboxmanage modifyhd /path/to/thedisk.vdi --compact
```

**With a Windows Host run this:**

```
VBoxManage.exe modifyhd c:\path\to\thedisk.vdi --compact
```

**With a Mac Host run this:**

```
VBoxManage modifyhd /path/to/thedisk.vdi --compact
```