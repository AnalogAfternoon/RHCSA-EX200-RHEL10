# Lesson 29 Lab — Using Remote Filesystems and Autofs

Complete the following tasks. Do not refer to your notes.

1. Install the `nfs-utils` package.

2. Enable and start the `nfs-server` service.

3. Create a directory called `/exports/data` to share over NFS.

4. Edit `/etc/exports` to share `/exports/data` with read/write access to all clients.

5. Apply the export changes without restarting the NFS server.

6. View the current active exports.

7. Open the firewall to allow NFS traffic permanently.

8. From a client machine, show what a server is exporting (use YOUR_SERVER_IP as a placeholder).

9. Mount the NFS share from the server to `/mnt/nfsdata` temporarily.

10. Add the NFS mount to `/etc/fstab` to make it persistent.

11. Install `autofs` and enable the service.

12. Configure autofs so that accessing `/misc/data` automatically mounts `YOUR_SERVER_IP:/exports/data`.
