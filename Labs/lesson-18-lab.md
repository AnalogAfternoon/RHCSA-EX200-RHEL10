# Lesson 18 Lab — Working with Partitions and Mounts

Complete the following tasks. Do not refer to your notes.

1. List all block devices on the system in a tree view.

2. List all block devices including their filesystem type and UUID.

3. Using `fdisk`, create a new partition on an available disk (use `/dev/sdb` as an example).

4. Create an XFS filesystem on the new partition `/dev/sdb1`.

5. Create a mount point at `/data`.

6. Mount `/dev/sdb1` to `/data` temporarily.

7. Verify the mount was successful.

8. Get the UUID of `/dev/sdb1`.

9. Add an entry to `/etc/fstab` to mount `/dev/sdb1` permanently using its UUID.

10. Test your fstab entry without rebooting.

11. Create a swap partition on `/dev/sdb2`, activate it, and verify it is active.
