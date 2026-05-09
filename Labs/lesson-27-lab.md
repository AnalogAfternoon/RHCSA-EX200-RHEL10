# Lesson 27 Lab — Securing RHEL with SELinux

Complete the following tasks. Do not refer to your notes.

1. Display the current SELinux mode.

2. Temporarily switch SELinux to permissive mode.

3. Switch SELinux back to enforcing mode.

4. Display the SELinux context of files in `/var/www/html/`.

5. Display the SELinux context of the running `sshd` process.

6. Create a file in `/tmp` called `webfile.html`, move it to `/var/www/html/`, and restore its correct SELinux context.

7. List all defined SELinux file context rules for `/var/www`.

8. Add a persistent SELinux file context rule for the directory `/mywebsite` so it is labeled as `httpd_sys_content_t`.

9. Apply the new context rule to `/mywebsite`.

10. Check whether the `httpd_can_network_connect` boolean is on or off.

11. Turn the `httpd_can_network_connect` boolean on persistently.

12. View any recent SELinux denial messages in the audit log.
