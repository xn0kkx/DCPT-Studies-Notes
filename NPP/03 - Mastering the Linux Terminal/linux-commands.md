# Essential Linux Commands

A curated list of common Linux commands, each with a detailed explanation and usage example.

---

## Searching & Text Processing

### `grep -v "pattern"`
Print lines **not** matching the given pattern.
```bash
grep -v "error" /var/log/syslog
```

### `grep -E -v "pattern"`
Extended-regex variant of `grep`; `-v` inverts the match.
```bash
grep -E -v "foo|bar" file.txt
```

### `grep -E "foo|bar|baz"`
Match any of the listed patterns using extended regex.
```bash
grep -E "WARN|ERROR|CRITICAL" /var/log/app.log
```

### `awk -F":" '{ print $1, $6 }' /etc/passwd`
Use `:` as field separator; print field 1 (username) and field 6 (home directory).
```bash
awk -F: '{ print $1, $6 }' /etc/passwd
```

### `cut -d":" -f1,6 /etc/passwd`
Use `:` as delimiter; extract fields 1 and 6 (username and home directory).
```bash
cut -d: -f1,6 /etc/passwd
```

### `sed 's/old/new/' file.txt`
Replace the **first** occurrence of `old` with `new` on each line (outputs to stdout). To edit in place, add `-i`:
```bash
sed -i 's/root/admin/' /etc/passwd
```

### `find /path -name "*.log" -mtime -7`
Search for `*.log` files under `/path` modified in the last 7 days.
```bash
find /var/log -name "*.log" -mtime -7
```

---

## File & Archive Management

### `tar -czvf archive.tar.gz /dir`
Create a gzip-compressed archive.
```bash
tar -czvf backup.tar.gz /etc /var/www
```

### `tar -xzvf archive.tar.gz -C /restore`
Extract a gzip-compressed archive into `/restore`.
```bash
tar -xzvf backup.tar.gz -C /restore
```

### `zip -r files.zip folder/`
Create a ZIP archive recursively.
```bash
zip -r project.zip src/ docs/
```

### `unzip archive.zip -d extracted/`
Extract a ZIP archive into `extracted/`.
```bash
unzip project.zip -d extracted/
```

---

## File Operations

### `cp -r src/ dest/`
Copy files or directories recursively.
```bash
cp -r ~/workspace/myapp /backup/myapp
```

### `mv oldname newname`
Move or rename files/directories.
```bash
mv temp.txt archive/temp.txt
```

### `rm -rf path/`
Remove files or directories recursively **without** prompt.
```bash
rm -rf /tmp/old-files
```

### `mkdir -p /path/to/dir`
Create a directory tree, including parent directories.
```bash
mkdir -p ~/logs/2025/April
```

### `chmod 755 script.sh`
Set permissions: owner rwx (7), group rx (5), others rx (5).
```bash
chmod 755 deploy.sh
```

### `chown user:group file.txt`
Change file owner and group.
```bash
chown www-data:www-data /var/www/html/index.html
```

---

## System Monitoring

### `ps aux`
List all running processes with details.
```bash
ps aux | grep httpd
```

### `top`
Interactive real-time process viewer.
```bash
top
```

### `htop`
Enhanced, interactive process viewer (if installed).
```bash
htop
```

### `df -h`
Show disk usage of mounted filesystems in human-readable format.
```bash
df -h
```

### `du -sh /path`
Display total size of a directory in human-readable form.
```bash
du -sh /var/log
```

### `ss -tulnp`
List all listening sockets with program names.
```bash
ss -tulnp
```

---

## Networking & Connectivity

### `ping -c 4 host`
Send 4 ICMP echo requests to check reachability.
```bash
ping -c 4 google.com
```

### `traceroute host`
Show the network path packets take to a host.
```bash
traceroute github.com
```

### `curl -I URL`
Fetch only HTTP headers from a URL.
```bash
curl -I https://api.example.com/status
```

### `wget URL`
Download a file from the web.
```bash
wget https://downloads.example.com/tool.tar.gz
```

### `ssh user@host`
Connect to a remote host via SSH.
```bash
ssh admin@192.168.1.10
```

### `scp file user@host:/remote/path`
Securely copy files to/from a remote host.
```bash
scp backup.sql root@dbserver:/backups/
```

### `rsync -avz src/ dest/`
Efficiently synchronize files/directories between locations.
```bash
rsync -avz /home/user/ www-data@web:/var/www/html/
```

---

## Services & Logs

### `systemctl status service`
Show status of a systemd service.
```bash
systemctl status nginx
```

### `systemctl restart|start|stop service`
Control systemd services.
```bash
systemctl restart sshd
systemctl stop apache2
```

### `journalctl -u service`
View logs for a specific systemd unit.
```bash
journalctl -u mysql.service --since "2 hours ago"
```

### `journalctl -f`
Follow the system journal in real time.
```bash
journalctl -f
```

---

## Viewing Files

### `cat file.txt`
Display entire file to stdout.
```bash
cat /etc/hosts
```

### `head -n 10 file.txt`
Show the first 10 lines of a file.
```bash
head -n 10 /var/log/messages
```

### `tail -n 10 file.txt`
Show the last 10 lines of a file.
```bash
tail -n 10 /var/log/syslog
```

### `tail -f file.log`
Follow appended data in real time.
```bash
tail -f /var/log/nginx/access.log
```

### `less file.txt`
Browse large files page by page.
```bash
less /var/log/auth.log
```
