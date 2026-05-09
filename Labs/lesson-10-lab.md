# Lesson 10 Lab — Securing Files with Permissions

Complete the following tasks. Do not refer to your notes.

---

1. Create a directory called `/project` and a group called `devs`. Set `/project` to be owned by the `devs` group.

2. Configure `/project` so that any file created inside it automatically inherits the `devs` group (SGID).

3. Set permissions on `/project` so the owner and group have full access, and others have no access.

4. Create a file inside `/project` and verify it inherits the `devs` group.

5. Check your current umask value.

6. Set the umask to `027` for the current session.

7. Create a new file and verify its default permissions reflect the new umask.

8. Find the `/tmp` directory and confirm it has the sticky bit set.

9. Create a world-writable directory called `/shared` and apply the sticky bit to it.

10. Verify the permissions on `/shared` show the sticky bit.
