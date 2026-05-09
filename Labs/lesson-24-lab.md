# Lesson 24 Lab — Managing SSH

Complete the following tasks. Do not refer to your notes.

1. Generate an SSH key pair on your local machine.

2. Copy your public key to a remote server (use YOUR_SERVER_IP as a placeholder).

3. Connect to the remote server using key-based authentication.

4. Start the `ssh-agent` and add your private key to it.

5. Edit `/etc/ssh/sshd_config` to disable direct root login. Restart sshd to apply.

6. Copy a local file called `report.txt` to the remote server's `/tmp` directory using `scp`.

7. Copy a remote file `/var/log/messages` from the server to your local `/tmp` directory.

8. Synchronize a local directory called `myproject/` to the remote server's home directory using `rsync`.
