# Lesson 19 Lab — Managing Advanced Storage

Complete the following tasks. Do not refer to your notes.

1. Initialize `/dev/sdb` as a physical volume.

2. Create a volume group called `myvg` using `/dev/sdb`.

3. Create a logical volume called `mylv` with a size of 5GB inside `myvg`.

4. Create an XFS filesystem on the logical volume.

5. Mount the logical volume to `/mnt/data` persistently via `/etc/fstab`.

6. Extend the logical volume by 2GB.

7. Grow the XFS filesystem to use the new space.

8. List all physical volumes, volume groups, and logical volumes.

9. Create a Stratis pool called `mypool` using `/dev/sdc`.

10. Create a Stratis filesystem called `myfs` inside `mypool`.

11. List all Stratis pools and filesystems.
