Make sure you have a `/mnt/hgfs` directory made and empty. If not:

```
sudo mkdir -p /mnt/hgfs
```

To mount the filesystem, run:

```
sudo mount -t fuse.vmhgfs-fuse .host:/ /mnt/hgfs -o allow_other
```

The shared folders will now be in subdirectories of `/mnt/hgfs`

Add the following line to `/etc/fstab`:

```
.host://mnt/hgfsfuse.vmhgfs-fuseauto,allow_other
```