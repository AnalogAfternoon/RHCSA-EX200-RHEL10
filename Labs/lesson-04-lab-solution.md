# Lesson 4 Lab — Solutions

1. Create `rhcsa-practice` directory.
```bash
mkdir ~/rhcsa-practice
```

2. Create subdirectories.
```bash
mkdir ~/rhcsa-practice/scripts ~/rhcsa-practice/logs ~/rhcsa-practice/backups
```

3. Create `readme.txt`.
```bash
touch ~/rhcsa-practice/readme.txt
```

4. Copy `readme.txt` to `backups`.
```bash
cp ~/rhcsa-practice/readme.txt ~/rhcsa-practice/backups/
```

5. Move and rename `readme.txt` to `logs/info.txt`.
```bash
mv ~/rhcsa-practice/readme.txt ~/rhcsa-practice/logs/info.txt
```

6. Create compressed tar archive.
```bash
tar -cvzf backup.tar.gz ~/rhcsa-practice
```

7. Extract archive into `/tmp`.
```bash
tar -xvf backup.tar.gz -C /tmp
```

8. Delete the directory.
```bash
rm -r ~/rhcsa-practice
```
