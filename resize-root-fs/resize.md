## Resizing Filesystem on First Boot

1. **Boot** -> `/etc/rc.local` -> `/etc/resize-root-fs`:
   
2. **Enlarge Partition Table for Partition 2**
   - Create the script `/etc/init.d/resize_root_fs` and install it as a service.
   - Delete the line `/etc/resize-root-fs` from `rc.local`.
   - Delete `/etc/resize-root-fs`.

3. **Reboot**

---

After rebooting, the service is executed once:
- `/etc/init.d/resize_root_fs` runs, resizing the filesystem.
- Uninstall the `root_fs` service.
- Delete the file `/etc/init.d/resize_root_fs`.
- **Service Exit** (No idea why exit code 3).


I have modified the resize-root-fs Skript to allow resizing to e.g. only 15 GB 
on a large SSD 
where you dont want to use the complete Space for Raspi Filesystem. 
To resize to a defined size modify the 2 files in the image before the first boot:

- /etc/rc.local File: add the desired size im MB 
- copy the new resize-root-fs to /etc

```bash
#!/bin/sh -e

/etc/resize-root-fs 15000
exit 0
```
Todo: integrate the modified resize-root-fs in image-backup


