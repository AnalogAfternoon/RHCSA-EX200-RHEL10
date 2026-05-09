# Lesson 24 Lab — Solutions

1. Generate SSH key pair.
```bash
ssh-keygen
```

2. Copy public key to remote server.
```bash
ssh-copy-id user@YOUR_SERVER_IP
```

3. Connect using key-based auth.
```bash
ssh user@YOUR_SERVER_IP
```

4. Start ssh-agent and add key.
```bash
eval $(ssh-agent)
ssh-add ~/.ssh/id_rsa
```

5. Disable root login in sshd_config.
```bash
sudo vim /etc/ssh/sshd_config
# Set: PermitRootLogin no
sudo systemctl restart sshd
```

6. Copy file to remote `/tmp`.
```bash
scp report.txt user@YOUR_SERVER_IP:/tmp/
```

7. Copy remote file to local `/tmp`.
```bash
scp user@YOUR_SERVER_IP:/var/log/messages /tmp/
```

8. Sync local directory to remote.
```bash
rsync -avz myproject/ user@YOUR_SERVER_IP:~/myproject/
```
