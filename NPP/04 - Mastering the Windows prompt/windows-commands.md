# Essential Windows Command-Line Commands

A curated list of commonly used Windows command-line instructions, each with a detailed description and example usage.

---

## File & Directory Operations

### `echo %cd%`
**Description:** Displays the current working directory.
```bat
echo %cd%
```

### `echo Text > file.txt` / `echo Text >> file.txt`
**Description:** Writes `Text` to `file.txt`. Use `>` to overwrite, `>>` to append.
```bat
echo Hello, world! > greeting.txt
echo Additional line >> greeting.txt
```

### `type file.txt`
**Description:** Displays the contents of `file.txt`.
```bat
type greeting.txt
```

### `copy source.txt dest.txt`
**Description:** Copies a file from `source.txt` to `dest.txt`. Can also copy multiple files.
```bat
copy report.docx backup_report.docx
```

### `move source dest`
**Description:** Moves or renames files and directories.
```bat
move temp.log ..\Archive\temp.log
```

### `del file.txt`
**Description:** Deletes `file.txt`. Use wildcards (`*`) to delete multiple files.
```bat
del obsolete_*.log
```

### `rmdir dirname` / `rmdir /S dirname`
**Description:** Removes an empty directory (`rmdir dirname`) or a directory tree with all contents (`/S`). Use `/Q` for quiet mode.
```bat
rmdir tempFolder
rmdir /S /Q OldBackups
```

### `dir /A` / `dir /S filename`
**Description:** Lists directory contents. `/A` shows hidden and system files; `/S filename` searches for `filename` in the current directory and all subdirectories.
```bat
dir /A
dir /S notes.txt
```

### `attrib +h file.txt` / `attrib -h file.txt`
**Description:** Sets (`+h`) or clears (`-h`) the hidden attribute on a file or directory.
```bat
attrib +h secret.txt
attrib -h secret.txt
```

---

## Text Editing & Environment Variables

### `notepad file.txt`
**Description:** Opens `file.txt` in Notepad GUI editor.
```bat
notepad greeting.txt
```

### `set`
**Description:** Displays all environment variables or sets a new one (`set VAR=value`).
```bat
set
set PROJECT_DIR=C:\Projects\MyApp
```

### `echo %VAR%`
**Description:** Displays the value of an environment variable.
```bat
echo %PROJECT_DIR%
```

### `whoami`
**Description:** Shows the current user name and domain.
```bat
whoami
```

### `hostname`
**Description:** Displays the computer’s name.
```bat
hostname
```

---

## System Information & Networking

### `ipconfig /all`
**Description:** Displays full TCP/IP configuration details.
```bat
ipconfig /all
```

### `ipconfig /flushdns`
**Description:** Clears the DNS resolver cache.
```bat
ipconfig /flushdns
```

### `netstat -n`
**Description:** Shows active TCP connections with numerical addresses.
```bat
netstat -n
```

### `netstat -ano`
**Description:** Lists all connections and listening ports, including owning process ID (PID).
```bat
netstat -ano
```

### `ping host -n 4`
**Description:** Sends 4 ICMP echo requests to `host`.
```bat
ping google.com -n 4
```

### `tracert host`
**Description:** Traces the route to `host`, showing each hop.
```bat
tracert github.com
```

### `pathping host`
**Description:** Combines `ping` and `tracert`, showing packet loss at each hop.
```bat
pathping microsoft.com
```

### `nslookup host`
**Description:** Queries DNS to obtain domain name or IP address mapping.
```bat
nslookup example.com
```

### `systeminfo`
**Description:** Displays detailed system configuration and OS information.
```bat
systeminfo
```

### `getmac`
**Description:** Shows MAC addresses for network adapters.
```bat
getmac /v /fo list
```

---

## Process & Service Management

### `tasklist`
**Description:** Lists current running processes with PID and memory usage.
```bat
tasklist
```

### `taskkill /PID 1234 /F`
**Description:** Terminates process with PID 1234 forcefully (`/F`).
```bat
taskkill /PID 1234 /F
```

### `sc query servicename`
**Description:** Queries the status of a Windows service.
```bat
sc query wuauserv
```

### `net start` / `net stop`
**Description:** Starts or stops a service by name.
```bat
net start wuauserv
net stop Spooler
```

### `net user`
**Description:** Displays all local user accounts.
```bat
net user
```

### `net user username`
**Description:** Shows detailed info for `username`.
```bat
net user JohnDoe
```

### `net user username password /add`
**Description:** Adds a new user `username` with specified `password`.
```bat
net user NewUser P@ssw0rd /add
```

### `net user username /delete`
**Description:** Deletes the user account `username`.
```bat
net user OldUser /delete
```

### `net use`
**Description:** Manages network shares and drive mappings.
```bat
net use Z: \\Server\Share /persistent:yes
```

---

## Maintenance & Utilities

### `chkdsk C: /F`
**Description:** Checks drive `C:` for file system errors and fixes them (`/F`).
```bat
chkdsk C: /F
```

### `sfc /scannow`
**Description:** Scans and repairs protected system files using Windows File Protection.
```bat
sfc /scannow
```

### `gpupdate /force`
**Description:** Applies Group Policy changes immediately.
```bat
gpupdate /force
```

### `shutdown /s /t 0`
**Description:** Shuts down the computer immediately (`/s`) with no delay (`/t 0`).
```bat
shutdown /s /t 0
```

### `schtasks /query`
**Description:** Displays scheduled tasks.
```bat
schtasks /query /fo LIST
```

### `wmic logicaldisk get name,size,freespace`
**Description:** Lists all logical disks with total size and free space via WMI.
```bat
wmic logicaldisk get name,size,freespace
```

---

