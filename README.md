**D E V O P S E N G I N E E R ' S R E F E R E N C E** 

# **Complete Linux & Networking Commands Handbook** 

## **for DevOps Engineers** 

_A practical, beginner-to-advanced reference for daily work, troubleshooting, automation, cloud infrastructure, CI/CD, containers, Kubernetes, and production incident response._ 

Linux  •  Networking  •  Bash  •  Git  •  Docker  •  Kubernetes  •  Terraform  •  Ansible  •  Cloud CLI  •  SRE 

Edition 2026 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **Table of Contents** 

|**1. Introducton**...............................................................................................................................................5|
|---|
|**2. Scope and Coverage**...................................................................................................................................5|
|**3. Linux Commands — Beginner Level**..........................................................................................................6|
|**4. Users and Groups**.....................................................................................................................................19|
|**5. Process Management**.............................................................................................................................. 23|
|**6. Disk and Storage Commands**................................................................................................................... 28|
|**7. Archiving and Compression**.....................................................................................................................33<br>|
|**8. System Informaton**.................................................................................................................................35|
|**9. Systemd and Services**.............................................................................................................................. 38|
|**10. Log Management**...................................................................................................................................40|
|**11. Bash and Shell Commands**.....................................................................................................................42|
|**12. Cron and Scheduling**..............................................................................................................................45|
|**13. Package Management**........................................................................................................................... 47|
|**14. Environment Variables**..........................................................................................................................49|
|**15. SSH and Remote Management**..............................................................................................................50|
|**16. Networking Commands — Complete Secton**.......................................................................................54|
|**17. curl and wget**......................................................................................................................................... 60|
|**18. Firewall and Security Networking**.........................................................................................................63|
|**19. tcpdump — Detailed Secton**.................................................................................................................65|
|**20. nmap**......................................................................................................................................................67<br>|
|**21. Network Troubleshootng**......................................................................................................................68|
|**22. Git Commands for DevOps**....................................................................................................................70|
|**23. Docker Commands**.................................................................................................................................74|
|**24. Docker Compose**.................................................................................................................................... 80|
|**25. Kubernetes Commands**..........................................................................................................................81|
|**26. Cloud CLI Commands**.............................................................................................................................86|
|**27. Terraform CLI**.........................................................................................................................................89|
|**28. Ansible Commands**................................................................................................................................92|
|**29. CI/CD Commands**................................................................................................................................... 95|
|**30. Monitoring and Performance Commands**.............................................................................................96|
|**31. Advanced Linux Commands**...................................................................................................................98|
|**32. DevOps Troubleshootng Playbooks**...................................................................................................100|
|**33. Real-World DevOps Command Workfows**.........................................................................................112|
|**34. Command Comparison Tables**.............................................................................................................113|
|**35. Top 100 Commands Every DevOps Engineer Should Know**................................................................116|
|**36. DevOps Command Cheat Sheet**...........................................................................................................121|



Page 2 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**37. Linux & Networking Commands — DevOps Interview Questons**......................................................124|
|---|
|**38. DevOps Learning Roadmap**................................................................................................................. 128|



Page 3 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **How to Use This Handbook** 

This handbook is organized to work two ways: as a linear learning path (read front to back to build DevOps competency from beginner to advanced) and as a fast lookup reference during real work (jump straight to a chapter, command, or the condensed cheat sheet in Chapter 36). 

Every important command follows the same consistent format: Purpose, Syntax, Example, Explanation, DevOps Use Case, Common Options, a Real-World Example, and Important Notes. Secondary/supporting commands use a shorter compact format with a description and example. Watch for the highlighted CAUTION boxes — they flag commands that are destructive, security-sensitive, or risky to run against production systems. 

- New to DevOps? Start at Chapter 3 and work through sequentially — each chapter builds on the last. 

- Preparing for an interview? Go straight to Chapter 37 (Interview Questions) after skimming the chapters that feel less familiar. 

- Troubleshooting a live incident? Jump to Chapter 32 (Troubleshooting Playbooks) or Chapter 21/25 for network/Kubernetes-specific chains. 

- Need a fast lookup during work? Chapter 36 (Cheat Sheet) is organized by category for quick scanning. 

**Note:** Commands shown with a sudo/root note require elevated privileges. Placeholders like <server-ip>, <username>, <pod-name>, and <container-id> should be replaced with your actual values — never copy example values (including any shown IPs or usernames) directly into production systems. 

Page 4 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **1. Introduction** 

Linux and networking command fluency is the operational backbone of DevOps and Site Reliability Engineering. Cloud platforms, Kubernetes, and CI/CD pipelines all ultimately run on Linux servers and containers, communicate over TCP/IP networks, and get debugged with the same core toolkit that's existed for decades. This handbook consolidates that toolkit into one practical reference — commands you will actually use, explained with real production context rather than abstract theory. 

### **2. Scope and Coverage** 

This handbook spans five layers of DevOps work: 

1. Linux fundamentals — the filesystem, permissions, users, processes, and storage. 

2. System administration — services (systemd), logs, scheduling, packages, and shell scripting. 

3. Networking — from basic connectivity checks through DNS, firewalls, packet capture, and structured troubleshooting. 

4. The DevOps toolchain — Git, Docker, Kubernetes, Terraform, Ansible, cloud CLIs, and CI/CD. 

5. Production operations — monitoring, performance analysis, and a full set of incident troubleshooting playbooks. 

Page 5 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **3. Linux Commands — Beginner Level** 

This chapter covers the core Linux commands every DevOps engineer touches daily: navigating the filesystem, managing files, viewing content, searching, processing text, and controlling permissions. Master these first — almost everything else in this handbook builds on them. 

#### **3.1 Navigation** 

##### **`pwd`** 

**Purpose:** Prints the full absolute path of the current working directory. 

###### **Syntax:** 

`pwd [options]` **Example:** `pwd` 

**Explanation:** With no options, pwd prints the logical path (respecting symlinks). `pwd -P` prints the physical path, resolving symlinks to their real location. 

**DevOps Use Case:** Used constantly in scripts to confirm where a script or deployment process is executing, and in CI/CD pipelines to sanity-check the working directory before running build or deploy commands. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-L|Print the logical path (default, respects symlinks)|
|-P|Print the physical path (resolves symlinks)|



###### **Real-World Example:** 

```
cd /var/www/app && pwd -P
```

**Note:** In shell scripts, prefer `$(pwd)` or `$PWD` cautiously — `$PWD` is a shell variable and can be stale if the directory was renamed underneath the shell. 

##### **`ls`** 

**Purpose:** Lists files and directories. 

###### **Syntax:** 

```
ls [options] [path]
```

###### **Example:** 

```
ls -la /etc
```

**Explanation:** `-l` gives a long listing (permissions, owner, size, date). `-a` shows hidden files (dotfiles). `-h` makes sizes human-readable. `-t` sorts by modification time, `-S` by size. 

**DevOps Use Case:** Verifying deployed artifacts exist, checking file permissions after a chmod/chown, inspecting log directories, confirming config files were copied by configuration management tools. 

Page 6 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-l|Long format listng|
|-a|Show hidden fles|
|-h|Human-readable sizes (with -l)|
|-t|Sort by modifcaton tme|
|-R|Recursive listng|
|-S|Sort by fle size|



###### **Real-World Example:** 

```
ls -lath /var/log/nginx | head -20
```

**Note:** `ls -l` output columns: permissions, link count, owner, group, size, modified date, name. 

##### **`cd`** 

**Purpose:** Changes the current working directory. 

###### **Syntax:** 

```
cd [directory]
```

###### **Example:** 

```
cd /opt/app
cd ..
cd -
cd ~
```

**Explanation:** `cd -` returns to the previous directory. `cd ~` or bare `cd` goes to the home directory. `cd ..` moves up one level. 

**DevOps Use Case:** Navigating between application, config, and log directories during troubleshooting sessions on a remote server. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-|Switch to previous directory|
|~|Go to home directory|



###### **Real-World Example:** 

```
cd /var/log && cd -
```

###### **`tree`** 

Displays a directory structure as an indented tree. Not installed by default on all distros (`apt install tree` / `dnf install tree`). 

Page 7 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
tree -L 2 /opt/app
tree -a -I 'node_modules|.git'
```

_Tip: Great for quickly understanding an unfamiliar project or deployment directory layout._ 

##### **`find`** 

**Purpose:** Searches for files and directories recursively based on name, type, size, time, permissions, and more. 

###### **Syntax:** 

```
find [path] [expression]
```

###### **Example:** 

```
find /var/log -name "*.log" -mtime +7
```

**Explanation:** Traverses the directory tree from `path`, testing each file against the expression. Supports actions like `- delete`, `-exec`. 

**DevOps Use Case:** Cleaning up old log files, finding large files eating disk space, locating config files across a filesystem, finding files by permission for security audits. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-name|Match by flename (case-sensitve)|
|-iname|Case-insensitve name match|
|-type f|d|Restrict to fles or directories|
|-mtme -n/+n|Modifed less/more than n days ago|
|-size +100M|Files larger than 100MB|
|-perm|Match by permission bits|
|-exec cmd {} \;|Run a command on each match|
|-delete|Delete matches (dangerous)|



###### **Real-World Example:** 

```
find /var/log -type f -name "*.log" -mtime +30 -exec rm {} \;
find / -xdev -size +500M -exec ls -lh {} \;
```

**CAUTION — Production Risk:** `-delete` and `-exec rm` are destructive and irreversible. Always run the same `find` without `-delete` first to review matches before deleting in production. 

###### **`locate`** 

Finds files by name using a prebuilt index database (mlocate/plocate), making it far faster than `find` for whole-filesystem searches. 

```
locate nginx.conf
sudo updatedb   # refresh the index
```

_Tip: The index updates on a schedule (usually daily via cron); newly created files may not appear until `updatedb` runs._ 

Page 8 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **3.2 File Management** 

###### **`touch`** 

Creates an empty file if it doesn't exist, or updates its access/modification timestamps if it does. 

```
touch app.log
touch -d "2026-01-01" file.txt
```

###### **`mkdir`** 

Creates directories. 

```
mkdir /opt/releases
mkdir -p /opt/app/releases/v1.2.3/logs
```

_Tip: `-p` creates parent directories as needed and does not error if the directory already exists — always use `-p` in deployment scripts._ 

##### **`cp`** 

**Purpose:** Copies files and directories. 

###### **Syntax:** 

```
cp [options] source destination
```

###### **Example:** 

```
cp -r /opt/app/config /opt/app/config.bak
```

**Explanation:** `-r` copies directories recursively. `-p` preserves permissions, ownership, and timestamps. `-a` (archive) is equivalent to `-dR --preserve=all`, ideal for backups. 

**DevOps Use Case:** Backing up config files before editing them, copying build artifacts between release directories, staging files before a deployment. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-r|Recursive (for directories)|
|-p|Preserve mode, ownership, tmestamps|
|-a|Archive mode — preserve everything, recursive|
|-v|Verbose|
|-i|Prompt before overwrite|
|-u|Copy only when source is newer|



###### **Real-World Example:** 

```
cp -a /etc/nginx/nginx.conf /etc/nginx/nginx.conf.$(date +%F)
```

**Note:** Always back up a config file (`cp file file.bak`) before editing it in production. 

###### **`mv`** 

Moves or renames files and directories. 

Page 9 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
mv app.log app.log.old
mv /tmp/build/* /opt/app/
```

_Tip: `mv` is atomic on the same filesystem — this is why release directories are often swapped with `mv` (or a symlink swap) instead of copying._ 

##### **`rm`** 

**Purpose:** Removes files or directories. 

###### **Syntax:** 

```
rm [options] file...
```

###### **Example:** 

```
rm old.log
rm -rf /opt/app/tmp/
```

**Explanation:** `-r` removes directories recursively, `-f` forces removal without prompting and ignores nonexistent files. **DevOps Use Case:** Cleaning up temporary build artifacts, old releases, and stale files in automated pipelines. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-r|Recursive|
|-f|Force, no prompts|
|-i|Interactve, prompt for each fle|
|-v|Verbose|



###### **Real-World Example:** 

```
find /opt/releases -maxdepth 1 -mtime +30 -exec rm -rf {} \;
```

**CAUTION — Production Risk:** `rm -rf` is one of the most dangerous commands in Linux — there is no recycle bin. Never run `rm -rf /` or `rm -rf $VAR/` where `$VAR` could be empty (it expands to `rm -rf /`). Double-check the path, especially when scripting with variables. 

###### **`rmdir`** 

Removes empty directories only (fails if the directory has contents — a safer alternative to `rm -r` for cleanup scripts). 

```
rmdir /opt/app/empty_dir
```

###### **`file`** 

Identifies the type of a file by inspecting its content (magic bytes), not just its extension. 

```
file app.bin
file /etc/passwd
```

###### **`stat`** 

Displays detailed metadata about a file: size, permissions, owner, inode number, and access/modify/change timestamps. 

```
stat /etc/nginx/nginx.conf
```

_Tip: Useful for confirming exactly when a config file was last modified during an incident review._ 

Page 10 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **3.3 Viewing Files** 

###### **`cat`** 

Prints entire file contents to stdout. Also used to concatenate multiple files. 

```
cat /etc/os-release
cat file1 file2 > combined.txt
```

###### **`tac`** 

Like `cat` but prints lines in reverse order (last line first). Handy for reading logs newest-first. 

```
tac /var/log/syslog | head -50
```

##### **`less`** 

**Purpose:** Views file content one screen at a time, with search and backward navigation. 

**Syntax:** 

```
less [options] file
```

###### **Example:** 

```
less /var/log/syslog
```

**Explanation:** Unlike `more`, `less` allows scrolling backward, searching with `/pattern`, and doesn't load the whole file into memory, so it handles huge log files well. 

**DevOps Use Case:** The default way to page through large log files during troubleshooting without flooding the terminal. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|/patern|Search forward|
|?patern|Search backward|
|n / N|Next / previous match|
|G|Jump to end of fle|
|g|Jump to start|
|-N|Show line numbers|



###### **Real-World Example:** 

```
journalctl -u nginx | less
```

###### **`more`** 

Simple pager, forward-only. Mostly superseded by `less`, but still available on minimal systems. 

```
more /etc/services
```

Page 11 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

##### **`head`** 

**Purpose:** Prints the first N lines (default 10) of a file. 

###### **Syntax:** 

```
head [options] file
```

###### **Example:** 

```
head -n 50 /var/log/app.log
```

**Explanation:** `-n` sets the number of lines; `-c` sets a byte count instead. 

**DevOps Use Case:** Quickly inspecting the beginning of a log file or CSV header without opening the whole file. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-n N|Show frst N lines|
|-c N|Show frst N bytes|



###### **Real-World Example:** 

```
head -n 20 /etc/passwd
```

##### **`tail`** 

**Purpose:** Prints the last N lines (default 10) of a file, with the option to follow it live as it grows. 

###### **Syntax:** 

```
tail [options] file
```

###### **Example:** 

```
tail -f /var/log/nginx/error.log
```

**Explanation:** `-f` follows the file in real time — the single most-used log command in DevOps. `-n` controls how many lines to show initially. 

**DevOps Use Case:** Live-tailing application or web server logs during a deployment or incident to watch for errors in real time. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-f|Follow fle as it grows|
|-F|Follow, and retry if fle is rotated/recreated|
|-n N|Show last N lines|
|-n +N|Start from line N|



###### **Real-World Example:** 

```
tail -F /var/log/nginx/error.log | grep -i error
```

Page 12 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**Note:** Prefer `-F` over `-f` when watching logs that get rotated (e.g., by logrotate), since `-F` reopens the file by name. 

###### **`nl`** 

Numbers the lines of a file. 

```
nl /etc/hosts
```

#### **3.4 Searching** 

##### **`grep`** 

**Purpose:** Searches for lines matching a pattern (plain text or regular expression) inside files or piped input. 

###### **Syntax:** 

```
grep [options] pattern [file...]
```

**Example:** `grep -i "error" /var/log/app.log` 

**Explanation:** The single most important text-search tool in Linux. `-i` ignores case, `-r` searches recursively, `-v` inverts the match (show non-matching lines), `-n` shows line numbers, `-E` enables extended regex, `-c` counts matches. 

**DevOps Use Case:** Finding error messages in logs, searching source code or config files for a string, filtering output of other commands (`ps aux | grep nginx`), auditing config files for a setting. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-i|Case-insensitve|
|-r / -R|Recursive search|
|-v|Invert match|
|-n|Show line numbers|
|-c|Count matching lines|
|-l|List only flenames with matches|
|-E|Extended regex|
|-A N / -B N / -C N|N lines afer/before/around match|
|--color=auto|Highlight matches|



###### **Real-World Example:** 

```
grep -rn "TODO" /opt/app/src/
grep -A 5 "Traceback" /var/log/app.log
```

**Note:** `ps aux | grep nginx` will also match the grep process itself; use `ps aux | grep '[n]ginx'` or `pgrep nginx` to avoid it. 

Page 13 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **`egrep`** 

Equivalent to `grep -E` (extended regular expressions, supporting `+`, `?`, `|`, `{}` without escaping). Considered legacy syntax — prefer `grep -E`. 

```
egrep "error|warn|fail" app.log
```

###### **`fgrep`** 

Equivalent to `grep -F` (fixed-string search, no regex interpretation — faster for literal strings). Prefer `grep -F`. 

```
fgrep "192.168.1.10" access.log
```

##### **`xargs`** 

**Purpose:** Builds and executes command lines from standard input, turning a list of items into arguments for another command. 

###### **Syntax:** 

```
command | xargs [options] target-command
```

###### **Example:** 

```
find /tmp -name "*.tmp" | xargs rm -f
```

**Explanation:** Many commands (like `rm`, `docker`) don't read filenames from stdin directly — `xargs` bridges that gap. `-I{}` lets you place each item explicitly; `-n1` runs the target command once per item; `-P` runs in parallel. 

**DevOps Use Case:** Bulk-deleting matched files, bulk-stopping/removing Docker containers, running the same command across a list of servers. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-I {}|Placeholder for each input item|
|-n N|Max N arguments per command invocaton|
|-P N|Run N processes in parallel|
|-0|Use null-terminated input (pairs with `fnd -print0`)|



###### **Real-World Example:** 

```
docker ps -aq | xargs docker rm -f
find . -name "*.log" -print0 | xargs -0 -I{} gzip {}
```

**Note:** Combine `find -print0` with `xargs -0` when filenames may contain spaces or newlines. 

#### **3.5 Text Processing** 

###### **`sort`** 

Sorts lines of text alphabetically or numerically. 

```
sort file.txt
sort -n -r numbers.txt
du -sh /var/* | sort -rh
```

Page 14 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

_Tip: `-h` sorts human-readable sizes (10K, 1M, 1G) correctly._ 

###### **`uniq`** 

Removes or counts duplicate adjacent lines. Almost always used after `sort`. 

```
sort access.log | uniq -c | sort -rn | head
```

###### **`cut`** 

Extracts columns/fields from each line, by character position or delimiter. 

```
cut -d':' -f1 /etc/passwd
cut -c1-10 file.txt
```

###### **`tr`** 

Translates or deletes characters from stdin. 

```
cat file.txt | tr 'a-z' 'A-Z'
echo "a,b,c" | tr ',' '\n'
```

##### **`awk`** 

**Purpose:** A full pattern-scanning and text-processing language, ideal for column-based data extraction and reporting. 

###### **Syntax:** 

```
awk 'pattern { action }' file
```

**Example:** `awk '{print $1, $4}' access.log` 

**Explanation:** AWK splits each line into fields (`$1`, `$2`, ...; `$0` is the whole line) using whitespace by default (`-F` sets another delimiter). Supports conditionals, loops, and built-in variables like `NR` (line number) and `NF` (number of fields). 

**DevOps Use Case:** Parsing structured log lines (like Nginx/Apache access logs) to extract IPs, status codes, or response times; generating quick reports from CSV/columnar output. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-F|Set the feld separator|
|'{print $N}'|Print feld N|
|NR|Current record (line) number|
|NF|Number of felds on the line|



###### **Real-World Example:** 

```
awk -F',' '{sum+=$3} END {print sum}' costs.csv
awk '$9==500 {print $1}' access.log | sort | uniq -c
```

**Note:** For quick one-off column extraction `awk` is usually simpler than `cut` because it handles variable whitespace automatically. 

Page 15 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

##### **`sed`** 

**Purpose:** Stream editor for filtering and transforming text, most commonly for find-and-replace. **Syntax:** 

```
sed [options] 'script' file
```

###### **Example:** 

```
sed 's/foo/bar/g' file.txt
```

**Explanation:** `s/pattern/replacement/flags` substitutes text; `g` replaces all matches on a line, not just the first. `-i` edits the file in place. `-n '2,5p'` prints a range of lines. 

**DevOps Use Case:** Bulk-editing config files in automation scripts (e.g., changing a port number or hostname across many files), stripping or transforming log lines before analysis. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-i|Edit fle in place|
|-e|Add multple script expressions|
|-n|Suppress automatc printng (used with `p`)|
|s/x/y/g|Substtute all occurrences of x with y|



###### **Real-World Example:** 

```
sed -i.bak 's/^Port 22$/Port 2222/' /etc/ssh/sshd_config
```

**Note:** Always use `-i.bak` (or a manual backup) instead of bare `-i` when editing production config files, so you can revert instantly if the substitution is wrong. 

###### **`paste`** 

Merges lines from multiple files side by side, column-wise. 

```
paste hosts.txt ips.txt
```

###### **`column`** 

Formats input into neatly aligned columns — great for making raw CSV or delimited output human-readable. 

```
column -t -s',' data.csv
```

#### **3.6 File Permissions & Ownership** 

Every file and directory in Linux has three permission sets — owner, group, and others — each with read (r), write (w), and execute (x) permissions. 

|**Symbol**|**Numeric**|**Meaning**|
|---|---|---|
|r|4|Read: view fle contents / list directory|
|w|2|Write: modify fle / create-delete fles in directory|
|x|1|Execute: run fle as program / enter directory ('cd' into it)|



Page 16 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

Permissions are shown as a 10-character string, e.g. `-rwxr-xr--`: the first character is the file type (`-` file, `d` directory, `l` symlink), then three groups of rwx for owner, group, and others. 

##### **`chmod`** 

**Purpose:** Changes file or directory permissions. 

###### **Syntax:** 

```
chmod [options] mode file
```

###### **Example:** 

```
chmod 755 script.sh
chmod +x deploy.sh
```

**Explanation:** Numeric mode: add r(4)+w(2)+x(1) per group, e.g. 755 = rwxr-xr-x. Symbolic mode: `u/g/o/a` (user/group/other/all) with `+/-/=` and `r/w/x`, e.g. `chmod u+x,go-w file`. 

**DevOps Use Case:** Making deployment/build scripts executable, locking down sensitive config files (e.g., private keys to 600), setting correct permissions after extracting an archive. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-R|Recursive|
|+x|Add execute permission|
|-w|Remove write permission|
|=|Set exact permission|



###### **Real-World Example:** 

```
chmod 600 ~/.ssh/id_rsa
chmod -R 755 /opt/app/scripts
```

**Note:** Never use `chmod 777` in production — it grants full read/write/execute to everyone, a serious security risk. Use the minimum permissions required. 

##### **`chown`** 

**Purpose:** Changes the owning user and/or group of a file or directory. 

###### **Syntax:** 

```
chown [options] user[:group] file
```

###### **Example:** 

```
chown user:group file.txt
```

**Explanation:** Can set user only, group only (`chown :group file`), or both. `-R` applies recursively. 

**DevOps Use Case:** Fixing ownership after deploying files as root so the application (running as a non-root service user) can read/write them; correcting ownership after copying files between servers. **Common Options:** 

Page 17 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|-R|Recursive|
|user:group|Set both owner and group|
|:group|Set group only|



###### **Real-World Example:** 

```
chown -R appuser:appgroup /opt/app/releases/current
```

**Note:** Requires root/sudo unless you own both the file and are a member of the target group (system-dependent). 

###### **`chgrp`** 

Changes only the group ownership of a file (a focused subset of `chown`). 

```
chgrp -R devops /opt/app/logs
```

###### **`umask`** 

Sets the default permission mask subtracted from new files/directories. Default `umask 022` gives new files 644 and new directories 755. 

```
umask
umask 027
```

#### **3.7 Special Permissions** 

|**Bit**|**On fles**|**On directories**|**Set with**|
|---|---|---|---|
|SUID (4000)|Runs the executable with the fle<br>owner's privileges (e.g.<br>`passwd`)|No efect|chmod u+s fle|
|SGID (2000)|Runs with the group's privileges|New fles inherit the directory's<br>group|chmod g+s dir|
|Stcky bit (1000)|No efect|Only the fle owner can<br>delete/rename fles inside (e.g.<br>`/tmp`)|chmod +t dir|



**CAUTION — Production Risk:** SUID binaries are a common privilege-escalation vector. Regularly audit SUID/SGID files with `find / -perm -4000 -type f 2>/dev/null` and remove the bit from anything that doesn't need it. 

Page 18 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **4. Users and Groups** 

Linux is a multi-user system with strict privilege separation. DevOps engineers use these commands to create service accounts, manage SSH access, and administer sudo privileges safely. 

#### **4.1 Identity & Session Commands** 

###### **`whoami`** 

Prints the current effective username. 

```
whoami
```

###### **`id`** 

Shows the current (or specified) user's UID, GID, and group memberships. 

```
id
id deploy
```

###### **`who`** 

Lists users currently logged in, their terminal, and login time. 

```
who
```

###### **`w`** 

Like `who` but also shows what each logged-in user is currently running and system load. 

```
w
```

###### **`users`** 

Prints a simple space-separated list of logged-in usernames. 

```
users
```

###### **`last`** 

Shows login history from /var/log/wtmp — useful for security auditing. 

```
last -n 20
last reboot
```

###### **`groups`** 

Shows which groups a user belongs to. 

```
groups deploy
```

#### **4.2 Managing Users and Groups** 

##### **`useradd`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Creates a new user account. 

**Syntax:** 

Page 19 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
useradd [options] username
```

###### **Example:** 

```
sudo useradd -m -s /bin/bash deploy
```

**Explanation:** `-m` creates a home directory; `-s` sets the login shell; `-G` adds supplementary groups; `-r` creates a system account (for services, no login). 

**DevOps Use Case:** Creating a dedicated, unprivileged service account to run an application instead of running it as root — a core production security practice. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-m|Create home directory|
|-s|Set login shell|
|-G|Supplementary groups|
|-r|System account (no password login, no expiry)|
|-u|Specify UID|



###### **Real-World Example:** 

```
sudo useradd -r -s /usr/sbin/nologin -M appsvc
```

**Note:** On Debian/Ubuntu, `adduser` is a friendlier interactive wrapper around `useradd`. 

###### **`usermod`** 

Modifies an existing user's account (shell, groups, lock/unlock). 

```
sudo usermod -aG docker deploy
sudo usermod -L deploy   # lock account
```

_Tip: Always use `-aG` (append) not `-G` alone — `-G` without `-a` replaces all existing group memberships._ 

###### **`userdel`** 

Deletes a user account. 

```
sudo userdel -r deploy
```

_Tip: `-r` also removes the user's home directory and mail spool._ 

##### **`passwd`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Sets or changes a user's password, or manages password aging/locking. 

###### **Syntax:** 

```
passwd [options] [username]
```

**Example:** 

```
sudo passwd deploy
```

Page 20 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**Explanation:** Without a username, changes the current user's password. `-l`/`-u` lock/unlock an account. `-e` forces password expiry on next login. 

**DevOps Use Case:** Resetting access for a service account, or locking an account during offboarding. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-l|Lock account|
|-u|Unlock account|
|-e|Expire password immediately|
|-S|Show password status|



###### **Real-World Example:** 

```
sudo passwd -l former_employee
```

###### **`groupadd`** 

Creates a new group. 

```
sudo groupadd devops
```

###### **`groupmod`** 

Renames or changes the GID of a group. 

```
sudo groupmod -n newname oldname
```

###### **`groupdel`** 

Deletes a group. 

```
sudo groupdel devops
```

#### **4.3 Privilege Escalation** 

##### **`sudo`** 

**Purpose:** Executes a single command as another user (typically root), based on rules in /etc/sudoers. 

###### **Syntax:** 

```
sudo [options] command
```

###### **Example:** 

```
sudo systemctl restart nginx
```

**Explanation:** `sudo -i` starts a root login shell; `sudo -u user command` runs as a specific user; `sudo -l` lists what the current user is permitted to run. 

**DevOps Use Case:** The standard way to perform privileged operations without sharing the root password — every action is logged with the invoking user's identity (auditable, unlike shared `su`). 

**Common Options:** 

Page 21 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|-u user|Run as a specifc user|
|-i|Start an interactve root login shell|
|-l|List allowed commands|
|-k|Invalidate cached credentals|



###### **Real-World Example:** 

```
sudo -u postgres psql
```

**Note:** In production, prefer granular sudoers rules (specific commands) over blanket `ALL=(ALL) NOPASSWD:ALL` access. 

###### **`su`** 

Switches to another user's full session (with `su -` loading their environment). Requires the target user's password unless run as root. 

```
su - postgres
```

##### **`visudo`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Safely edits /etc/sudoers with syntax validation, preventing a broken file from locking everyone out of sudo. **Syntax:** 

```
visudo
```

**Example:** 

```
sudo visudo
```

**Explanation:** Opens the sudoers file in the default editor and validates syntax before saving; rejects the save if there's an error. 

**DevOps Use Case:** Granting a DevOps team passwordless sudo for specific service-restart commands, or adding a new admin. 

###### **Real-World Example:** 

```
sudo visudo -f /etc/sudoers.d/deploy
```

**CAUTION — Production Risk:** Never edit /etc/sudoers directly with a plain text editor — a syntax error can break sudo for every user on the box. 

Page 22 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **5. Process Management** 

Understanding processes — their IDs, states, and signals — is essential for diagnosing performance problems and stuck applications in production. 

#### **5.1 Core Concepts** 

|**Term**|**Meaning**|
|---|---|
|PID|Process ID — unique numeric identfer for a running process|
|PPID|Parent Process ID — the PID of the process that spawned it|
|Foreground process|Runs atached to the terminal; blocks further input untl it fnishes|
|Background process|Runs detached from terminal input (`&`); terminal remains free|
|Zombie process|Finished process stll in the process table because its parent hasn't read its exit status|
|Orphan process|Process whose parent has exited; gets re-parented to init/systemd (PID 1)|
|Signal|Sofware interrupt sent to a process (e.g. SIGTERM, SIGKILL, SIGHUP)|



#### **5.2 Viewing Processes** 

##### **`ps`** 

**Purpose:** Prints a snapshot of currently running processes. 

###### **Syntax:** 

`ps [options]` **Example:** `ps aux` 

**Explanation:** `aux` (BSD syntax) shows all processes for all users with full details: USER, PID, %CPU, %MEM, VSZ, RSS, STAT, START, TIME, COMMAND. `ps -ef` is the equivalent System V syntax. 

**DevOps Use Case:** Getting a one-time snapshot of what's running before killing or investigating a process; feeding into `grep`/`awk` in scripts. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|aux|All processes, user-oriented, full format|
|-ef|All processes, System V format|
|--sort=-%cpu|Sort by CPU usage descending|
|-o|Custom output columns|



###### **Real-World Example:** 

```
ps aux --sort=-%mem | head -10
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
```

Page 23 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**Note:** `ps aux | grep nginx` is common but also matches grep itself — use `pgrep nginx` for scripting. 

##### **`top`** 

**Purpose:** Real-time, interactive view of running processes and overall system resource usage. 

###### **Syntax:** 

```
top
```

###### **Example:** 

```
top
```

**Explanation:** Shows load average, CPU/memory summary, and a live-updating process table. Press `M` to sort by memory, `P` by CPU, `k` to kill a PID, `q` to quit. 

**DevOps Use Case:** First command run when investigating 'the server is slow' — quickly identifies the process(es) consuming CPU or memory. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|M|Sort by memory (interactve key)|
|P|Sort by CPU (interactve key)|
|-b|Batch mode (for scriptng/logging)|
|-n N|Number of iteratons in batch mode|



###### **Real-World Example:** 

```
top -b -n 1 | head -20
```

###### **`htop`** 

An interactive, color, mouse-enabled alternative to `top` with easier sorting, filtering, and tree view of processes. Not installed by default — `apt install htop` / `dnf install htop`. 

```
htop
```

###### **`pgrep`** 

Lists PIDs of processes matching a name/pattern, without the grep-matches-itself problem. 

```
pgrep -f nginx
pgrep -u www-data
```

##### **`kill`** 

**Purpose:** Sends a signal to a process by PID (default signal: SIGTERM, a graceful shutdown request). 

###### **Syntax:** 

```
kill [-signal] pid
```

**Example:** 

Page 24 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
kill 1234
kill -9 1234
```

**Explanation:** SIGTERM (15, default) asks the process to shut down gracefully. SIGKILL (9) forcibly terminates it immediately at the kernel level — the process cannot catch or ignore it. SIGHUP (1) often tells daemons to reload config. 

**DevOps Use Case:** Gracefully stopping a stuck application (SIGTERM first), and only using SIGKILL if it doesn't respond — abrupt SIGKILL can leave files/locks/DB transactions in a bad state. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-15 / -TERM|Graceful terminaton (default)|
|-9 / -KILL|Force kill, cannot be caught|
|-1 / -HUP|Hangup — ofen triggers confg reload|
|-l|List all available signal names|



###### **Real-World Example:** 

```
kill -TERM $(pgrep -f my-worker)
# wait a few seconds, then if still running:
kill -9 $(pgrep -f my-worker)
```

**CAUTION — Production Risk:** Always try SIGTERM before SIGKILL in production. `kill -9` skips cleanup handlers and can corrupt in-flight writes. 

###### **`killall`** 

Kills all processes matching a name (rather than a PID). 

```
killall -TERM nginx
```

###### **`pkill`** 

Like `kill` but matches by name/pattern (uses the same matching as `pgrep`). 

```
pkill -f "node server.js"
```

###### **`jobs`** 

Lists background/suspended jobs in the current shell session. 

```
jobs -l
```

###### **`bg`** 

Resumes a suspended job in the background. 

```
bg %1
```

###### **`fg`** 

Brings a background/suspended job to the foreground. 

```
fg %1
```

Page 25 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

##### **`nohup`** 

**Purpose:** Runs a command immune to hangups (SIGHUP), so it keeps running after the terminal/SSH session closes. **Syntax:** 

```
nohup command &
```

###### **Example:** 

```
nohup ./long_running_script.sh > out.log 2>&1 &
```

**Explanation:** Redirects output to nohup.out (or a specified file) and detaches the process from the controlling terminal's SIGHUP signal. 

**DevOps Use Case:** Running a one-off long migration or batch job over SSH without needing `tmux`/`screen`. 

###### **Real-World Example:** 

```
nohup ./backup.sh > /var/log/backup.log 2>&1 &
```

**Note:** For production services, prefer a proper systemd unit or process manager over `nohup` — it lacks restart-onfailure, log rotation, and boot persistence. 

###### **`nice`** 

Starts a process with a modified scheduling priority (-20 highest priority to 19 lowest). 

```
nice -n 10 ./batch_job.sh
```

###### **`renice`** 

Changes the priority of an already-running process. 

```
sudo renice -n 5 -p 1234
```

###### **`watch`** 

Repeatedly runs a command and shows live-updating output — turns any static command into a monitor. 

```
watch -n 2 'df -h'
watch -d 'kubectl get pods'
```

_Tip: `-d` highlights differences between updates._ 

##### **`lsof`** 

**Purpose:** Lists open files — and on Linux, 'everything is a file', so this also shows open network sockets, which process holds a lock, etc. 

###### **Syntax:** 

```
lsof [options]
```

###### **Example:** 

```
lsof -i :8080
```

**Explanation:** `-i :PORT` shows which process is using a TCP/UDP port. `-p PID` shows all files opened by a process. `-u user` filters by user. 

**DevOps Use Case:** Finding which process is bound to a port before starting a service that needs it ('address already in use' errors), or diagnosing 'too many open files' errors. 

Page 26 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-i :PORT|Processes using a port|
|-p PID|Files opened by a specifc PID|
|-u user|Files opened by a user|
|+D dir|Files open under a directory|



###### **Real-World Example:** 

```
sudo lsof -i :8080
lsof -p $(pgrep -f myapp) | wc -l
```

#### **5.3 Troubleshooting Scenario: 100% CPU** 

Scenario: A production application is consuming 100% CPU. Steps a DevOps engineer should take: 

6. Run `top` or `htop` to identify the offending PID and confirm CPU% and process name. 

7. Run `ps -p <PID> -o pid,ppid,cmd,%cpu,%mem,etime` to get process details and how long it has run. 

8. Check if it's a single runaway thread: `top -H -p <PID>` to see per-thread CPU usage. 

9. Check application logs (`journalctl -u <service>` or app logs) for the time the spike started — look for stuck loops, retry storms, or a traffic spike. 

10. If safe, capture a stack trace/profile (language-specific: `jstack` for Java, `py-spy dump` for Python) before restarting, to diagnose the root cause. 

11. Decide: restart the service (`systemctl restart <service>`) to restore availability, then investigate the captured diagnostics afterward. 

12. After mitigation, check `dmesg`/`journalctl -k` for OOM killer activity and review recent deploys/config changes as a likely trigger. 

Page 27 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **6. Disk and Storage Commands** 

#### **6.1 Core Concepts** 

- Partition — a logical division of a physical/virtual disk. 

- Filesystem — the structure (ext4, xfs, btrfs, etc.) used to organize data on a partition. 

- Mount point — the directory a filesystem is attached to and accessed through. 

- Inode — a data structure storing metadata about a file; a filesystem has a finite number of inodes, separate from disk space. 

#### **6.2 Disk Usage** 

##### **`df`** 

**Purpose:** Reports disk space usage per mounted filesystem. 

###### **Syntax:** 

```
df [options] [path]
```

###### **Example:** 

```
df -h
```

**Explanation:** `-h` shows human-readable sizes. `-i` shows inode usage instead of block usage — critical because a filesystem can be 'full' on inodes while having free space. 

**DevOps Use Case:** First command to check when you get a 'disk full' or 'no space left on device' error. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-h|Human-readable sizes|
|-i|Inode usage instead of blocks|
|-T|Show flesystem type|



###### **Real-World Example:** 

```
df -h
df -i /var
```

**Note:** `df` reports space based on the filesystem's own accounting, which can differ from `du`'s file-by-file sum (see below). 

##### **`du`** 

**Purpose:** Reports disk usage of files and directories by walking the directory tree. 

###### **Syntax:** 

```
du [options] [path]
```

**Example:** 

Page 28 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### `du -sh /var/*` 

**Explanation:** `-s` summarizes (total per argument instead of every subdirectory). `-h` human-readable. Combine with `sort -rh` to find the biggest space consumers. **DevOps Use Case:** Finding which directory or log file is consuming disk space when `df` reports low free space. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-s|Summarize (one total per path)|
|-h|Human-readable|
|-a|Include fles, not just directories|
|--max-depth=N|Limit recursion depth|



###### **Real-World Example:** 

```
du -sh /var/* | sort -rh | head -10
du -h --max-depth=1 /opt/app
```

**Note:** df vs du can disagree: `du` sums file sizes it can see, while `df` reflects actual filesystem block usage — a file deleted while still held open by a running process still consumes space that `df` counts but `du` (which only sees the directory tree) cannot. Restarting the process that holds the deleted file releases that space. Use `lsof +L1` or `lsof | grep deleted` to find such files. 

#### **6.3 Block Devices, Mounting & Filesystems** 

###### **`lsblk`** 

Lists block devices (disks, partitions) in a tree view with sizes and mount points. 

```
lsblk
lsblk -f   # include filesystem type and UUID
```

###### **`blkid`** 

Shows block device attributes: UUID, filesystem type, label. Used when writing /etc/fstab entries. 

```
sudo blkid
```

##### **`mount`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Attaches a filesystem to a directory (mount point), making it accessible. 

###### **Syntax:** 

```
mount [-t type] device mountpoint
```

###### **Example:** 

```
sudo mount /dev/sdb1 /mnt/data
```

Page 29 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**Explanation:** With no arguments, lists all currently mounted filesystems. Persistent mounts belong in /etc/fstab, not manual `mount` commands. 

**DevOps Use Case:** Attaching an additional EBS/disk volume, mounting an NFS share, or attaching an ISO/ image for troubleshooting. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-t type|Filesystem type (ext4, xfs, nfs...)|
|-o optons|Mount optons (ro, noexec, etc.)|
|-a|Mount everything in /etc/fstab|



###### **Real-World Example:** 

```
sudo mount -t nfs 10.0.0.5:/export /mnt/nfs
```

**Note:** A manual `mount` does not survive a reboot — add the entry to /etc/fstab for persistence, and always test with `mount -a` before rebooting to catch fstab typos. 

###### **`umount`** 

Detaches a mounted filesystem. Fails if the mount point is in use (`lsof +D /mnt/data` shows what's using it). 

```
sudo umount /mnt/data
```

###### **`findmnt`** 

Modern tool to query mounted filesystems in a tree view, filterable by mount point, source, or fstype. 

```
findmnt /var
```

###### **`fdisk`** 

Interactive partition table editor for MBR/GPT disks. 

```
sudo fdisk -l
sudo fdisk /dev/sdb
```

_Tip: Partitioning is destructive if done incorrectly — always confirm the target device with `lsblk` first._ 

###### **`parted`** 

Scriptable partition editor, better suited than fdisk for GPT and large disks (>2TB). 

```
sudo parted /dev/sdb print
```

##### **`mkfs`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Creates (formats) a filesystem on a partition or block device. 

###### **Syntax:** 

```
mkfs -t type /dev/device
```

**Example:** 

Page 30 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
sudo mkfs -t ext4 /dev/sdb1
```

**Explanation:** Variants exist per filesystem: `mkfs.ext4`, `mkfs.xfs`, `mkfs.vfat`. 

**DevOps Use Case:** Preparing a newly attached cloud disk volume before mounting it for the first time. 

###### **Real-World Example:** 

```
sudo mkfs.xfs /dev/nvme1n1
```

**CAUTION — Production Risk:** This is destructive — it erases all existing data on the target device. Triple-check the device name (`lsblk`) before running. 

###### **`fsck`** 

Checks and repairs filesystem consistency. Should generally be run on an unmounted filesystem. 

```
sudo fsck /dev/sdb1
```

_Tip: Running fsck on a mounted, in-use root filesystem can cause data loss — schedule it for boot time (`fsck -f` after unmounting, or via a rescue/recovery boot) instead._ 

##### **`dd`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Low-level utility that copies raw bytes between files, devices, or streams block-by-block. 

###### **Syntax:** 

```
dd if=source of=destination [options]
```

###### **Example:** 

```
sudo dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

**Explanation:** `if` is input file, `of` is output file, `bs` sets block size. Used for disk cloning, creating bootable USB drives, or zero-filling a disk. 

**DevOps Use Case:** Creating a disk image backup of a volume, or benchmarking raw disk write speed. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|if=|Input fle/device|
|of=|Output fle/device|
|bs=|Block size (afects speed)|
|status=progress|Show live progress|



###### **Real-World Example:** 

```
dd if=/dev/zero of=testfile bs=1M count=1024 status=progress
```

**CAUTION — Production Risk:** `dd` is nicknamed 'disk destroyer' for a reason: swapping `if`/`of` or targeting the wrong device can silently and irreversibly wipe a disk. Always double- and triple-check device names before running. 

Page 31 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **`sync`** 

Flushes filesystem buffers, writing cached data to disk immediately. 

###### `sync` 

_Tip: Often used before safely detaching a device or before a `dd` disk clone to ensure buffers are flushed._ 

Page 32 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **7. Archiving and Compression** 

##### **`tar`** 

**Purpose:** Bundles multiple files/directories into a single archive, optionally with compression. 

###### **Syntax:** 

```
tar [options] archive.tar target
```

###### **Example:** 

```
tar -czvf backup.tar.gz /opt/app/config
```

**Explanation:** `-c` create, `-x` extract, `-z` gzip compression, `-j` bzip2, `-J` xz, `-v` verbose, `-f` specifies the archive filename (must come last among flags). 

**DevOps Use Case:** Packaging application releases and config backups, transferring build artifacts between CI/CD stages, backing up before major changes. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-c|Create archive|
|-x|Extract archive|
|-t|List archive contents|
|-z|gzip compression (.tar.gz)|
|-j|bzip2 compression (.tar.bz2)|
|-v|Verbose|
|-C dir|Extract into a specifc directory|



###### **Real-World Example:** 

```
tar -czvf release-$(date +%F).tar.gz -C /opt/app .
tar -xzvf release.tar.gz -C /opt/app/releases/new
```

**Note:** Use `tar -tzvf archive.tar.gz` to preview contents before extracting into an important directory. 

###### **`gzip / gunzip`** 

Compresses/decompresses a single file with the gzip algorithm (.gz). 

```
gzip app.log
gunzip app.log.gz
```

###### **`zip / unzip`** 

Creates/extracts .zip archives, cross-platform-friendly (commonly used for Lambda packages, Windows-shared artifacts). 

```
zip -r app.zip ./dist
unzip app.zip -d /opt/app
```

###### **`bzip2`** 

Higher compression ratio than gzip but slower — used when archive size matters more than speed. 

Page 33 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
bzip2 largefile.log
```

###### **`xz`** 

Even higher compression ratio than bzip2, commonly used for distributing large software packages/kernel images. 

```
xz -9 largefile.tar
```

**Note:** For CI/CD build artifact archiving, `tar -czf` is the most portable default across Linux systems; use `zip` only if the consumer requires it (e.g. Windows tooling or AWS Lambda). 

Page 34 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **8. System Information** 

These commands answer 'what am I working with?' — kernel version, hardware, uptime, and resource totals. They're the first stop when onboarding onto an unfamiliar server. 

###### **`uname`** 

Prints system information: kernel name, version, architecture. 

```
uname -a
```

###### **`hostname`** 

Shows or sets the system's hostname. 

```
hostname
hostname -I   # show IP addresses
```

###### **`hostnamectl`** 

Modern systemd tool to view/set hostname and related metadata (OS, kernel, virtualization). 

```
hostnamectl
sudo hostnamectl set-hostname web01
```

##### **`uptime`** 

**Purpose:** Shows how long the system has been running, number of logged-in users, and load averages. 

###### **Syntax:** 

`uptime` **Example:** `uptime` 

**Explanation:** Load average shows 1/5/15-minute averages of the run queue length. A load average consistently higher than the number of CPU cores indicates the system is CPU-saturated. 

**DevOps Use Case:** A quick first-glance health check — high load average combined with slow response times points toward CPU or I/O contention. 

###### **Real-World Example:** 

```
uptime
nproc   # compare load average against core count
```

###### **`date`** 

Displays or sets the system date/time. 

```
date
date -u
date +%F
```

###### **`timedatectl`** 

Modern systemd tool for viewing/configuring system time, timezone, and NTP sync status. 

```
timedatectl
sudo timedatectl set-timezone UTC
```

Page 35 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

_Tip: Clock drift between servers breaks TLS, JWT validation, and distributed system consistency — always verify NTP sync (`timedatectl` shows 'System clock synchronized: yes')._ 

##### **`free`** 

**Purpose:** Displays total, used, and free physical and swap memory. 

###### **Syntax:** 

```
free [options]
```

###### **Example:** 

```
free -h
```

**Explanation:** `-h` human-readable. The 'available' column (not 'free') is the realistic estimate of memory available for new applications, since Linux uses free RAM for disk cache that can be reclaimed instantly. 

**DevOps Use Case:** Diagnosing memory pressure and OOM-kill risk; checking swap usage, which often signals memory exhaustion. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-h|Human-readable|
|-s N|Repeat every N seconds|
|-m / -g|Show in MB / GB|



###### **Real-World Example:** 

```
free -h -s 5
```

**Note:** Low 'free' but high 'available' is normal and healthy — Linux caches aggressively. Watch 'available' and swap usage, not raw 'free'. 

###### **`vmstat`** 

Reports virtual memory, process, CPU, and I/O statistics over an interval. 

```
vmstat 2 5
```

_Tip: High values in the 'si'/'so' (swap in/out) columns indicate memory pressure._ 

###### **`dmesg`** 

Prints kernel ring buffer messages — hardware events, driver issues, and notably OOM-killer activity. 

`dmesg -T | tail -50 dmesg | grep -i "out of memory"` _Tip: `-T` converts timestamps to human-readable form._ 

###### **`lscpu`** 

Displays detailed CPU architecture information (cores, threads, sockets, cache, virtualization support). 

```
lscpu
```

###### **`lsmem`** 

Displays memory ranges and their online/offline status. 

Page 36 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
lsmem
```

###### **`lsusb`** 

Lists connected USB devices — mostly relevant to bare-metal/on-prem infrastructure. 

```
lsusb
```

###### **`lspci`** 

Lists PCI devices — network cards, GPUs, storage controllers. Useful when diagnosing driver or hardware-passthrough issues. 

```
lspci | grep -i ethernet
```

##### **`journalctl`** 

**Purpose:** Queries logs collected by systemd's journal — the primary log viewer on modern Linux systems. 

###### **Syntax:** 

```
journalctl [options]
```

###### **Example:** 

```
journalctl -u nginx --since "1 hour ago"
```

**Explanation:** Covered in depth in the Logs and Systemd chapters. `-k` shows kernel messages (like dmesg); `-p err` filters by priority. 

**DevOps Use Case:** Central place to check system-wide and per-service logs on any systemd-based distro (Ubuntu 16.04+, RHEL 7+, Debian 8+). 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-u service|Logs for a specifc unit|
|-f|Follow (live tail)|
|--since / --untl|Time range flter|
|-p priority|Filter by priority (emerg..debug)|
|-k|Kernel messages only|
|-b|Logs since last boot|



###### **Real-World Example:** 

```
journalctl -k -p err -b
```

Page 37 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **9. Systemd and Services** 

systemd is the init system and service manager on virtually all modern Linux distributions. It starts services at boot, manages dependencies, restarts crashed services, and centralizes logging via the journal. 

#### **9.1 Key Concepts** 

|**Concept**|**Meaning**|
|---|---|
|Unit|A resource systemd manages — a service, socket, mount, tmer, etc. (defned in<br>a .service/.tmer/... fle)|
|Service|A unit type representng a background process/daemon|
|Target|A group of units representng a system state (e.g. mult-user.target ≈ old runlevel 3)|
|Enabled|Unit is confgured to start automatcally at boot|
|Actve|Unit is currently running|
|Failed|Unit exited with an error and did not recover|



#### **9.2 systemctl** 

##### **`systemctl`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** The primary command to start, stop, restart, enable, disable, and inspect systemd units. 

###### **Syntax:** 

```
systemctl [command] [unit]
```

###### **Example:** 

```
systemctl status nginx
```

**Explanation:** `status` shows current state, recent log lines, and the process tree. `start`/`stop`/`restart` control the running state; `reload` re-reads config without dropping connections (when the app supports it); `enable`/`disable` control boot-time autostart. 

**DevOps Use Case:** The single most-used command for managing any service — web servers, databases, custom app services, Docker daemon, etc. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|status|Show current state and recent logs|
|start / stop / restart|Control the running process|
|reload|Reload confg without full restart (if supported)|
|enable / disable|Control autostart at boot|
|is-actve|Print 'actve'/'inactve' (scriptable)|



Page 38 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|is-enabled|Print 'enabled'/'disabled' (scriptable)|
|--failed|List all failed units|
|daemon-reload|Reload unit fles afer editng them|



```
systemctl status nginx
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl reload nginx
systemctl enable nginx
systemctl disable nginx
systemctl is-active nginx
systemctl is-enabled nginx
systemctl --failed
sudo systemctl daemon-reload   # after editing a unit file
```

**Note:** After editing a .service file under /etc/systemd/system/, you must run `systemctl daemon-reload` before the change takes effect, and then `restart` the unit. 

#### **9.3 Troubleshooting a Failed Service** 

13. `systemctl status <service>` — check the exact failure reason and exit code shown at the bottom. 

14. `journalctl -u <service> -n 100 --no-pager` — read the last 100 log lines for stack traces or config errors. 

15. `journalctl -u <service> -p err -b` — filter to error-level messages since boot. 

16. Verify the config file syntax if the app has a `--test`/`-t` flag (e.g. `nginx -t`). 

17. Check dependent resources: disk space (`df -h`), required ports free (`ss -lntp`), permissions on data directories. 

18. After a fix, `sudo systemctl restart <service>` and re-check `status` and `is-active`. 

Page 39 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **10. Log Management** 

Almost every incident investigation starts and ends in the logs. This section covers the tools to read, filter, and manage log growth. 

###### **`zgrep`** 

Runs `grep` against gzip-compressed files without manually decompressing them first — essential for searching rotated/archived logs. 

```
zgrep -i "error" /var/log/nginx/error.log.2.gz
```

##### **`logrotate`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Automatically rotates, compresses, and eventually removes old log files to prevent disks from filling up. 

###### **Syntax:** 

```
logrotate [options] configfile
```

###### **Example:** 

```
sudo logrotate -f /etc/logrotate.conf
```

**Explanation:** Driven by config files under /etc/logrotate.d/ per application, specifying rotation frequency, retention count, compression, and post-rotation hooks (like signaling the app to reopen its log file). 

**DevOps Use Case:** Preventing 'disk full' incidents caused by unbounded application log growth; a standard piece of any production server setup. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-f|Force rotaton now (for testng)|
|-d|Debug mode (dry run, verbose)|



###### **Real-World Example:** 

```
sudo logrotate -d /etc/logrotate.d/nginx   # dry-run to verify config
```

**Note:** Applications that keep a log file open (instead of reopening it, e.g. via SIGHUP) will keep writing to the nowunlinked (deleted) file after rotation until restarted — this is a classic cause of 'df shows full but du doesn't match' (see Chapter 6). 

#### **10.1 Finding Errors Across Common Log Sources** 

```
# systemd-managed services
journalctl -u nginx
journalctl -u nginx --since "1 hour ago"
# Web servers
tail -f /var/log/nginx/error.log
tail -f /var/log/apache2/error.log      # Debian/Ubuntu
```

Page 40 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
tail -f /var/log/httpd/error_log        # RHEL/CentOS
# Application logs
grep -i "error" /var/log/application.log
grep -i "exception" /var/log/app/*.log
# System / kernel logs
journalctl -k -p err
cat /var/log/syslog     # Debian/Ubuntu
cat /var/log/messages   # RHEL/CentOS
# Authentication logs
tail -f /var/log/auth.log      # Debian/Ubuntu
tail -f /var/log/secure        # RHEL/CentOS
grep "Failed password" /var/log/auth.log
# Kubernetes / container logs
kubectl logs <pod-name>
kubectl logs <pod-name> -f --tail=100
docker logs -f <container-id>
```

**Note:** On RHEL/CentOS/Fedora, `/var/log/messages` and `/var/log/secure` are the equivalents of Debian/Ubuntu's `/var/log/syslog` and `/var/log/auth.log`. 

Page 41 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **11. Bash and Shell Commands** 

#### **11.1 Core Shell Concepts** 

|**Concept**|**Example**|**Meaning**|
|---|---|---|
|Variable|NAME=value|Local shell variable (no spaces around =)|
|Environment variable|export NAME=value|Variable passed to child processes|
|$PATH|echo $PATH|Colon-separated list of directories searched for<br>executables|
|Command substtuton|$(command)|Replace with the command's output|
|Pipe|cmd1 | cmd2|Send stdout of cmd1 as stdin to cmd2|
|Redirecton >|cmd > fle|Redirect stdout, overwrite fle|
|Redirecton >>|cmd >> fle|Redirect stdout, append to fle|
|Redirecton <|cmd < fle|Use fle as stdin|
|Stderr redirect 2>|cmd 2> err.log|Redirect stderr only|
|Combine streams 2>&1|cmd > all.log 2>&1|Redirect stderr to same place as stdout|
|&&|cmd1 && cmd2|Run cmd2 only if cmd1 succeeds (exit code 0)|
||||cmd1 || cmd2|Run cmd2 only if cmd1 fails|
|;|cmd1 ; cmd2|Run cmd2 regardless of cmd1's result|
|Exit code|echo $?|0 = success, non-zero = failure (checked afer any<br>command)|



##### **`tee`** 

**Purpose:** Reads stdin and writes it both to stdout and to one or more files simultaneously. 

###### **Syntax:** 

```
command | tee [options] file
```

###### **Example:** 

```
echo "hello" | tee output.txt
```

**Explanation:** `-a` appends instead of overwriting. Commonly chained with `sudo` when redirection alone can't write to a root-owned file (`echo x | sudo tee file` works; `sudo echo x > file` does not, because the redirection happens in the unprivileged shell). 

**DevOps Use Case:** Watching command output live while also saving it to a log file for later review — very common in deployment scripts. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-a|Append instead of overwrite|



Page 42 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Real-World Example:** 

```
./deploy.sh | tee -a /var/log/deploy.log
echo 'net.core.somaxconn=1024' | sudo tee -a /etc/sysctl.conf
```

#### **11.2 Environment & Utility Commands** 

###### **`echo`** 

Prints text/variables to stdout. 

```
echo "Deploying version $VERSION"
```

###### **`printf`** 

Formatted output, more predictable than `echo` for scripts needing precise formatting. 

```
printf "%s: %d\n" "count" 5
```

###### **`export`** 

Marks a shell variable as an environment variable, inheritable by child processes. 

```
export NODE_ENV=production
```

###### **`env`** 

Prints all environment variables, or runs a command with a modified environment. 

```
env
env NODE_ENV=production node app.js
```

###### **`printenv`** 

Prints the value of a specific environment variable (or all, like `env`). 

```
printenv PATH
```

###### **`source`** 

Executes a script in the current shell (not a subshell), so variable/function definitions persist. Also written as `.`. 

```
source .env
. ~/.bashrc
```

###### **`alias`** 

Creates a shortcut for a longer command. 

```
alias k='kubectl'
alias ll='ls -lah'
```

###### **`history`** 

Shows previously run commands from the shell history. 

```
history | grep docker
```

###### **`which`** 

Shows the full path of the executable that would run for a given command name. 

```
which python3
```

Page 43 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **`whereis`** 

Locates a binary, its source, and man page. 

```
whereis nginx
```

###### **`type`** 

Shows how a name would be interpreted — alias, builtin, function, or file. 

```
type ll
type cd
```

**Note:** Never hardcode secrets (API keys, passwords) in scripts that get committed to source control or that echo values to shell history/logs. Use environment variables sourced from a secrets manager, and add sensitive files to .gitignore. 

Page 44 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **12. Cron and Scheduling** 

##### **`crontab`** 

**Purpose:** Manages per-user scheduled jobs (cron table). 

###### **Syntax:** 

```
crontab [options]
```

###### **Example:** 

```
crontab -e
```

**Explanation:** `-e` edits the current user's crontab; `-l` lists it; `-r` removes it entirely. System-wide jobs also live in /etc/cron.d/, /etc/crontab, and /etc/cron.{hourly,daily,weekly,monthly}/. 

**DevOps Use Case:** Scheduling recurring maintenance tasks — backups, cleanup scripts, cache warmers, certificate renewal checks. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-e|Edit crontab|
|-l|List crontab|
|-r|Remove crontab|
|-u user|Operate on another user's crontab (as root)|



###### **Real-World Example:** 

|`crontab -l`|
|---|
|`sudo crontab -u appuser -l`|



**Note:** Cron jobs run with a minimal environment (no full $PATH, no login shell profile) — always use absolute paths to binaries and scripts inside cron jobs, and redirect output to a log file for debugging. 

###### Cron schedule syntax: 

```
*  *  *  *  *  command
|  |  |  |  |
|  |  |  |  +--- Day of week (0-6, Sun=0)
|  |  |  +------ Month (1-12)
|  |  +--------- Day of month (1-31)
|  +------------ Hour (0-23)
+--------------- Minute (0-59)
Examples:
0 2 * * *        # every day at 2:00 AM
*/15 * * * *     # every 15 minutes
0 0 * * 0        # every Sunday at midnight
0 9-17 * * 1-5   # every hour, 9am-5pm, weekdays
```

###### **`at`** 

Schedules a one-time job to run at a specific future time (unlike cron's recurring schedule). 

Page 45 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
echo "./cleanup.sh" | at 23:00
```

###### **`systemd timers`** 

Modern alternative to cron: a .timer unit paired with a .service unit. Offers better logging (via journalctl), dependency handling, and the ability to catch up on missed runs (`Persistent=true`). 

```
systemctl list-timers
systemctl status backup.timer
```

_Tip: Preferred over cron in modern systemd-based infrastructure for anything more than a trivial recurring task._ 

Page 46 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **13. Package Management** 

#### **13.1 Debian / Ubuntu (APT)** 

##### **`apt`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** The modern, user-friendly front end for managing .deb packages on Debian/Ubuntu. 

###### **Syntax:** 

```
apt [command] [package]
```

###### **Example:** 

```
sudo apt update && sudo apt install nginx
```

**Explanation:** `update` refreshes the package index (does not upgrade anything); `upgrade` installs newer versions of installed packages; `install`/`remove` manage individual packages; `search` finds packages by name/description. 

**DevOps Use Case:** Installing runtime dependencies, patching systems for CVEs, provisioning base images/Dockerfiles. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|update|Refresh package index|
|upgrade|Upgrade installed packages|
|install|Install a package|
|remove|Remove a package (keep confg)|
|purge|Remove a package and its confg|
|search|Search for a package|
|list --installed|List installed packages|



###### **Real-World Example:** 

```
sudo apt update && sudo apt install -y curl jq unzip
sudo apt list --installed | grep nginx
```

**Note:** Always run `apt update` before `install`/`upgrade` so you're resolving against the latest index; failing to do so can install stale or unavailable versions. 

###### **`apt-get`** 

The older, script-friendly APT front end. Functionally similar to `apt` but with more stable output formatting — many automation scripts still target `apt-get` for that reason. 

```
sudo apt-get update && sudo apt-get install -y nginx
```

###### **`dpkg`** 

Low-level tool that installs/queries individual .deb files directly (no dependency resolution or repositories). 

Page 47 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
sudo dpkg -i package.deb
dpkg -l | grep nginx
```

_Tip: Use `apt install ./package.deb` instead when possible — it resolves dependencies that plain `dpkg -i` will leave broken._ 

#### **13.2 RHEL / CentOS / Fedora (DNF/YUM)** 

##### **`dnf`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** The modern package manager for RHEL 8+/Fedora/CentOS Stream (successor to yum, same command surface). 

###### **Syntax:** 

```
dnf [command] [package]
```

###### **Example:** 

```
sudo dnf install nginx
```

**Explanation:** `check-update` lists available updates; `update`/`upgrade` applies them; `search` finds packages; `list installed` shows installed packages. 

**DevOps Use Case:** Same role as `apt` on the RHEL family — provisioning, patching, dependency management. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|install|Install a package|
|remove|Remove a package|
|update|Update all/specifc packages|
|search|Search for a package|
|list installed|List installed packages|
|repolist|List enabled repositories|



###### **Real-World Example:** 

```
sudo dnf install -y epel-release
sudo dnf update -y
```

###### **`yum`** 

Predecessor to dnf, still present (often as an alias to dnf) on RHEL 7/CentOS 7 and many current systems for compatibility. 

```
sudo yum install nginx
```

###### **`rpm`** 

Low-level tool for querying/installing individual .rpm files directly, analogous to `dpkg`. 

```
rpm -qa | grep nginx
sudo rpm -ivh package.rpm
```

Page 48 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **14. Environment Variables** 

|**File**|**Scope**|
|---|---|
|~/.bashrc|Per-user, loaded for interactve non-login shells|
|~/.profle / ~/.bash_profle|Per-user, loaded for login shells|
|/etc/environment|System-wide, simple KEY=value pairs (no shell syntax), loaded at login for<br>all users|
|/etc/profle, /etc/profle.d/*.sh|System-wide, loaded for login shells|



Common DevOps uses of environment variables: passing AWS credentials to the CLI/SDKs (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`), configuring an application (`NODE_ENV`, `DATABASE_URL`), injecting CI/CD pipeline variables (GitHub Actions secrets, GitLab CI/CD variables), and configuring Docker/Kubernetes containers via `-e`/`envFrom`/`ConfigMap`/`Secret`. 

```
export AWS_REGION=us-east-1
docker run -e NODE_ENV=production -e PORT=3000 myapp:latest
kubectl create secret generic db-creds --from-literal=password=<value>
```

**CAUTION — Production Risk:** Secrets should never be hardcoded in source code, committed to git, or passed as plain CLI arguments (visible in `ps aux` / shell history). Use a secrets manager (AWS Secrets Manager, Vault, Kubernetes Secrets) or CI/CD masked variables instead. 

Page 49 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **15. SSH and Remote Management** 

##### **`ssh`** 

**Purpose:** Opens a secure, encrypted shell session (or runs a single remote command) on a remote host. 

###### **Syntax:** 

```
ssh [options] user@host [command]
```

###### **Example:** 

```
ssh deploy@10.0.1.5
```

**Explanation:** Authenticates via password or (preferably) public-key cryptography. Can also tunnel ports and forward X11. 

**DevOps Use Case:** The primary way DevOps engineers access remote servers for troubleshooting, deployment, and administration. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-i keyfle|Use a specifc private key|
|-p port|Non-default SSH port|
|-L local:host:remote|Local port forwarding|
|-R remote:host:local|Remote port forwarding|
|-J jumphost|Connect via a jump/baston host|
|-v|Verbose (debug connecton issues)|



###### **Real-World Example:** 

```
ssh -i ~/.ssh/prod.pem -J bastion-user@bastion-host deploy@10.0.1.5
```

**Note:** Password authentication should be disabled in production (`PasswordAuthentication no` in sshd_config) in favor of key-based auth. 

##### **`scp`** 

**Purpose:** Securely copies files between hosts over SSH. 

###### **Syntax:** 

```
scp [options] source destination
```

###### **Example:** 

```
scp app.tar.gz deploy@10.0.1.5:/opt/app/
```

**Explanation:** Syntax mirrors `cp` but with `user@host:path` for remote endpoints. `-r` for directories. 

**DevOps Use Case:** Quick one-off file transfers to/from a server — deploying a single artifact, pulling a log file for local analysis. 

###### **Common Options:** 

Page 50 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|-r|Recursive|
|-P port|Non-default SSH port (capital P, unlike ssh's -p)|
|-i keyfle|Use a specifc private key|



###### **Real-World Example:** 

```
scp -i prod.pem deploy@10.0.1.5:/var/log/app.log ./local-app.log
```

**Note:** For repeated or large transfers, prefer `rsync` — it supports resuming and only transfers changed data. 

###### **`sftp`** 

Interactive secure file transfer shell over SSH (supports ls, get, put, cd like an FTP client, but encrypted). 

```
sftp deploy@10.0.1.5
```

##### **`rsync`** 

**Purpose:** Efficiently synchronizes files/directories locally or over SSH, transferring only the differences. 

###### **Syntax:** 

```
rsync [options] source destination
```

###### **Example:** 

```
rsync -avz --delete /opt/app/dist/ deploy@10.0.1.5:/opt/app/dist/
```

**Explanation:** `-a` archive mode (preserves permissions, symlinks, timestamps, recursive), `-v` verbose, `-z` compress in transit, `--delete` removes files on the destination that no longer exist on the source (mirroring). 

**DevOps Use Case:** Deploying application code/static assets to servers, backing up directories, syncing large log archives without re-copying unchanged files. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-a|Archive mode|
|-v|Verbose|
|-z|Compress during transfer|
|--delete|Mirror deletons on destnaton|
|--dry-run|Preview changes without applying|
|-e ssh -p port|Custom SSH port|



###### **Real-World Example:** 

```
rsync -avz --dry-run /opt/app/ deploy@10.0.1.5:/opt/app/   # preview first
```

**Note:** Always run `--dry-run` before using `--delete` against a production destination — it's easy to accidentally mirror- 

Page 51 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

delete files you meant to keep. 

##### **`ssh-keygen`** 

**Purpose:** Generates public/private SSH key pairs. 

###### **Syntax:** 

```
ssh-keygen [options]
```

###### **Example:** 

```
ssh-keygen -t ed25519 -C "deploy@ci"
```

**Explanation:** `-t` sets the key type (ed25519 recommended over older RSA for new keys); `-f` sets the output file path; `-C` adds a comment (usually an identifying label). 

**DevOps Use Case:** Creating a dedicated deploy key for CI/CD pipelines or a personal key for server access. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-t ed25519 / rsa|Key algorithm|
|-b bits|Key size (for RSA, e.g. 4096)|
|-f path|Output fle|
|-C comment|Label/comment|



###### **Real-World Example:** 

```
ssh-keygen -t ed25519 -f ~/.ssh/ci_deploy_key -N ""
```

###### **`ssh-copy-id`** 

Copies your public key to a remote server's ~/.ssh/authorized_keys, enabling passwordless key-based login. 

```
ssh-copy-id -i ~/.ssh/id_ed25519.pub deploy@10.0.1.5
```

###### **`ssh-agent / ssh-add`** 

`ssh-agent` runs in the background holding decrypted private keys in memory; `ssh-add` loads a key into it so you don't reenter its passphrase on every connection. 

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

#### **15.1 SSH Config, Jump Hosts, and Port Forwarding** 

A ~/.ssh/config file lets you define per-host shortcuts, including bastion/jump-host chaining: 

```
Host bastion
    HostName bastion.example.com
    User ops
    IdentityFile ~/.ssh/bastion_key
```

Page 52 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
Host appserver
    HostName 10.0.1.5
    User deploy
    IdentityFile ~/.ssh/prod_key
    ProxyJump bastion
```

With this config, `ssh appserver` automatically routes through the bastion host — no manual -J flag needed. 

|**Forwarding type**|**Flag**|**Use case**|
|---|---|---|
|Local forwarding|-L local_port:remote_host:remote_port|Access a remote-only service (e.g. an<br>internal DB) from your local machine|
|Remote forwarding|-R remote_port:local_host:local_port|Expose a local service to the remote<br>host/network|
|Dynamic (SOCKS) forwarding|-D local_port|Route arbitrary trafc through the SSH<br>tunnel as a SOCKS proxy|



```
# Access a remote DB on 5432 as if it were local, via a bastion
ssh -L 5432:db-internal.local:5432 -J bastion-user@bastion-host deploy@appserver
```

Page 53 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **16. Networking Commands — Complete Section** 

Networking is where most production incidents ultimately show up — a working application can still be unreachable because of DNS, routing, firewall, or load-balancer misconfiguration. This chapter builds a complete, layered toolkit. 

#### **16.1 Basic Network Commands** 

##### **`ip`** 

**Purpose:** The modern, all-in-one tool for viewing and configuring network interfaces, addresses, routes, and neighbors (replaces the deprecated `ifconfig`/`route`/`arp`). **Syntax:** 

```
ip [object] [command]
```

**Example:** 

```
ip addr show
```

**Explanation:** Objects include `addr` (IP addresses), `link` (interfaces up/down, MTU), `route` (routing table), and `neigh` (ARP/neighbor table). Covered in depth in section 11.2. 

**DevOps Use Case:** The default tool for all interface/routing inspection and configuration on modern Linux. 

###### **Real-World Example:** 

```
ip addr show eth0
```

###### **`ifconfig`** 

Legacy tool to view/configure network interfaces. Deprecated in favor of `ip`, but still present on many systems and widely recognized in older scripts/docs. 

```
ifconfig eth0
```

##### **`ping`** 

**Purpose:** Tests basic reachability and round-trip latency to a host using ICMP echo requests. 

###### **Syntax:** 

```
ping [options] host
```

**Example:** 

```
ping -c 4 8.8.8.8
```

**Explanation:** `-c N` sends N packets and stops (avoid an endless ping in scripts). Reports packet loss and round-trip time statistics. 

**DevOps Use Case:** The first, fastest check for 'is the network path even up' — before diving into DNS, firewall, or application-layer debugging. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-c N|Send N packets then stop|



Page 54 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|-i N|Interval between packets (seconds)|
|-W N|Timeout per reply|



###### **Real-World Example:** 

```
ping -c 4 example.com
```

**Note:** Many hosts/firewalls block ICMP entirely for security — a failed ping does not always mean the service itself is down; confirm with `curl`/`nc` at the application/transport layer too. 

###### **`tracepath`** 

Traces the network path to a host without requiring root privileges (unlike classic traceroute). 

```
tracepath example.com
```

##### **`traceroute`** 

**Purpose:** Shows the sequence of routers (hops) a packet passes through to reach a destination, with latency per hop. 

###### **Syntax:** 

```
traceroute host
```

###### **Example:** 

```
traceroute example.com
```

**Explanation:** Sends packets with increasing TTL values; each router that decrements TTL to 0 sends back an ICMP error, revealing the hop. Helps pinpoint where in the path latency or packet loss occurs. 

**DevOps Use Case:** Diagnosing where connectivity breaks or slows down between your server and a remote endpoint (e.g. an external API or another region). 

###### **Real-World Example:** 

```
traceroute -n example.com
```

**Note:** Not installed by default on all distros (`apt install traceroute` / `dnf install traceroute`); intermediate hops may show `* * *` if they block ICMP/UDP probes — that alone isn't necessarily a problem. 

###### **`mtr`** 

Combines `ping` and `traceroute` into a continuously updating live view per hop — much better for spotting intermittent packet loss than a single traceroute snapshot. 

```
mtr example.com
mtr -rw -c 100 example.com   # report mode, non-interactive
```

#### **16.2 IP and Interface Management** 

```
ip addr                 # show all interfaces and their IP addresses
ip addr show eth0       # show a specific interface
ip addr add 10.0.0.5/24 dev eth0     # add an IP address
```

Page 55 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
ip addr del 10.0.0.5/24 dev eth0     # remove an IP address
```

```
ip link                 # show interface link status (up/down, MTU, MAC)
ip link set eth0 up     # bring an interface up
ip link set eth0 down   # bring an interface down
ip route                # show the routing table
ip route add default via 10.0.0.1     # add a default gateway
ip route get 8.8.8.8    # show which route would be used for a destination
ip neigh                # show the ARP/neighbor table (IP-to-MAC mappings)
```

**Note:** Changes made with `ip addr`/`ip route` directly are not persistent across reboots — for permanent config use your distro's network manager (netplan, NetworkManager, /etc/network/interfaces, or nmcli), or you risk losing the configuration on the next reboot. 

#### **16.3 DNS** 

DNS record types you'll encounter regularly: 

|**Record**|**Purpose**|
|---|---|
|A|Maps a hostname to an IPv4 address|
|AAAA|Maps a hostname to an IPv6 address|
|CNAME|Aliases one hostname to another hostname|
|MX|Specifes mail servers for a domain|
|TXT|Arbitrary text — commonly used for domain verifcaton, SPF/DKIM|
|NS|Specifes the authoritatve name servers for a domain|
|PTR|Reverse DNS — maps an IP address back to a hostname|



##### **`dig`** 

**Purpose:** The primary DNS query tool for detailed lookups and troubleshooting. 

**Syntax:** 

```
dig [options] domain [record-type]
```

**Example:** 

```
dig example.com
```

**Explanation:** By default queries A records. Specify a record type explicitly (MX, TXT, NS, ...). `+short` gives a terse answer-only output, ideal for scripting. 

**DevOps Use Case:** Diagnosing DNS resolution problems, verifying DNS changes have propagated, checking mail/TXT records for domain verification. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|+short|Answer only, no verbose output|
|-x IP|Reverse DNS lookup (PTR)|



Page 56 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|@server|Query a specifc DNS server|
|+trace|Trace the full resoluton path from root servers|



###### **Real-World Example:** 

```
dig example.com A
dig example.com MX
dig -x 8.8.8.8
dig @8.8.8.8 example.com +short
```

###### **`nslookup`** 

Older, interactive-capable DNS lookup tool. Still widely available and used, though `dig` is generally preferred for scripting. 

```
nslookup example.com
nslookup example.com 8.8.8.8
```

###### **`host`** 

Simple, concise DNS lookup tool — quick alternative to `dig` for a one-line answer. 

```
host example.com
```

###### **`resolvectl`** 

Queries and manages systemd-resolved, showing which DNS servers are actually in effect per interface (useful since /etc/resolv.conf can be a symlink managed by systemd-resolved). 

```
resolvectl status
resolvectl query example.com
```

#### **16.4 Ports and Connections** 

##### **`ss`** 

**Purpose:** Displays socket statistics — the modern replacement for `netstat`, much faster on systems with many connections. 

###### **Syntax:** 

```
ss [options]
```

###### **Example:** 

```
ss -tulpn
```

**Explanation:** `-t` TCP, `-u` UDP, `-l` listening sockets only, `-p` show the owning process, `-n` show numeric ports/addresses instead of resolving names. 

**DevOps Use Case:** Checking which ports are listening before deploying a service, confirming a service actually bound to the expected interface/port, counting established connections. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-t|TCP sockets|



Page 57 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|-u|UDP sockets|
|-l|Listening sockets only|
|-p|Show owning process (needs sudo for other users' processes)|
|-n|Numeric output (skip DNS/service name resoluton)|
|-a|All sockets (listening and non-listening)|



###### **Real-World Example:** 

```
sudo ss -tulpn
ss -tn state established
```

**Note:** Prefer `ss` over `netstat` on modern systems — `netstat` is deprecated in `net-tools` and may not even be installed by default. 

###### **`netstat`** 

Legacy socket/routing statistics tool. Functionally overlaps with `ss` and `ip route`; still recognized from muscle memory and older documentation. 

```
netstat -tulpn
```

##### **`nc`** 

**Purpose:** Netcat — a general-purpose tool for reading/writing raw TCP or UDP connections; the 'Swiss army knife' of networking. 

###### **Syntax:** 

```
nc [options] host port
```

###### **Example:** 

```
nc -zv example.com 443
```

**Explanation:** `-z` performs a port-scan-style connection test without sending data (zero-I/O mode); `-v` verbose; `-u` for UDP. Can also act as a simple listener (`nc -l port`) for quick testing. 

**DevOps Use Case:** Quickly verifying whether a specific TCP port is reachable from a given host — e.g. confirming a security group/firewall rule actually allows the intended traffic. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-z|Scan mode — check connectvity without sending data|
|-v|Verbose|
|-u|UDP instead of TCP|
|-w N|Timeout in seconds|
|-l|Listen mode|



Page 58 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Real-World Example:** 

```
nc -zv db-server.internal 5432
nc -zv -w 3 api.example.com 443
```

###### Determining what's listening, and whether a port is reachable: 

```
sudo ss -tulpn | grep 8080      # which process is listening on 8080?
sudo lsof -i :8080              # alternative view of the same
nc -zv example.com 443          # is the port open from here?
curl -v telnet://example.com:443  # another way to test raw TCP connect
```

|**Concept**|**Meaning**|
|---|---|
|Listening|A process has bound to a port and is waitng for incoming connectons|
|Established|An actve, two-way connected TCP session|
|TCP|Connecton-oriented, reliable, ordered delivery (HTTP, SSH, databases)|
|UDP|Connectonless, no delivery guarantee, lower overhead (DNS, video/voice, some<br>metrics protocols)|



Page 59 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **17. curl and wget** 

##### **`curl`** 

**Purpose:** Transfers data to/from a URL over HTTP, HTTPS, FTP, and many other protocols — the primary tool for API testing and HTTP debugging. 

###### **Syntax:** 

```
curl [options] url
```

###### **Example:** 

```
curl -I https://example.com
```

**Explanation:** `-I` fetches headers only (HEAD request). `-v` shows the full request/response including TLS handshake details. `-X` sets the HTTP method. `-H` adds a header. `-d`/`--data` sends a request body. 

**DevOps Use Case:** Testing REST APIs, checking load balancer/health-check endpoints, verifying TLS certificates, debugging webhook deliveries, smoke-testing a deployment. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-I|Headers only (HEAD request)|
|-v|Verbose — show full request/response and TLS handshake|
|-X METHOD|Set HTTP method (GET/POST/PUT/DELETE...)|
|-H|Add a request header|
|-d / --data|Send a request body|
|-o fle|Write response body to a fle|
|-s|Silent (no progress meter)|
|-L|Follow redirects|
|-w '%{htp_code}'|Print just the status code (great for scriptng/health checks)|
|-k|Skip TLS certfcate verifcaton (debugging only, insecure)|



**Note:** Avoid `-k` in production scripts — skipping TLS verification defeats the purpose of HTTPS and should only be used temporarily while debugging a known cert issue. 

```
curl example.com
curl -I example.com
curl -v https://example.com
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name": "svc"}'
curl -H "Authorization: Bearer <token>" https://api.example.com/status
curl -o /dev/null -s -w "%{http_code}\n" https://example.com/health
```

Page 60 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **17.1 HTTP Status Codes at a Glance** 

|**Range**|**Meaning**|
|---|---|
|2xx|Success (200 OK, 201 Created, 204 No Content)|
|3xx|Redirecton (301 Moved Permanently, 302 Found, 304 Not Modifed)|
|4xx|Client error (400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 429 Too<br>Many Requests)|
|5xx|Server error (500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable, 504<br>Gateway Timeout)|



##### **`wget`** 

**Purpose:** Downloads files over HTTP/HTTPS/FTP; designed for retrieving and saving content rather than API interaction. 

###### **Syntax:** 

```
wget [options] url
```

###### **Example:** 

```
wget https://example.com/release.tar.gz
```

**Explanation:** Supports resuming interrupted downloads (`-c`), recursive site mirroring, and background downloading — strengths curl doesn't emphasize. 

**DevOps Use Case:** Downloading release artifacts, installers, or reference files inside a Dockerfile or provisioning script. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-O fle|Save with a specifc flename|
|-c|Contnue/resume a partal download|
|-q|Quiet mode|
|--limit-rate=|Throtle download speed|



###### **Real-World Example:** 

```
wget -q https://releases.example.com/app-1.4.0.tar.gz -O app.tar.gz
```

#### **17.2 curl vs wget** 

||**curl**|**wget**|
|---|---|---|
|Primary strength|API testng, arbitrary HTTP methods,<br>headers|File downloading, recursive fetch, resuming|
|Default behavior|Prints response to stdout|Saves response to a fle|



Page 61 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

||**curl**|**wget**|
|---|---|---|
|Protocol range|Very broad (HTTP, FTP, SMTP, LDAP, etc.)|Mainly HTTP/HTTPS/FTP|
|Best for|curl -X POST ... to test an endpoint|wget htps://.../installer.sh to fetch and<br>save|



Page 62 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **18. Firewall and Security Networking** 

Linux firewall tooling filters inbound/outbound traffic by port, protocol, and source/destination — the last line of network-level defense before traffic reaches (or leaves) an application. 

###### **`ufw`** 

Uncomplicated Firewall — a simplified front end for iptables, the default on Ubuntu. 

```
sudo ufw allow 22/tcp
sudo ufw allow from 10.0.0.0/24 to any port 5432
sudo ufw status verbose
```

###### **`firewalld`** 

Zone-based dynamic firewall manager, the default on RHEL/CentOS/Fedora. Uses `firewall-cmd` and supports runtime changes without dropping existing connections. 

```
sudo firewall-cmd --add-port=8080/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

##### **`iptables`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** The classic, low-level Linux packet-filtering tool, operating on chains of rules (INPUT, OUTPUT, FORWARD) within tables (filter, nat, mangle). 

###### **Syntax:** 

```
iptables [-t table] command chain rule -j target
```

###### **Example:** 

```
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

**Explanation:** `-A` appends a rule, `-p` protocol, `--dport` destination port, `-j` the target action (ACCEPT/DROP/REJECT). Rules are evaluated top to bottom per chain. 

**DevOps Use Case:** Fine-grained packet filtering on legacy systems, or where `nftables` isn't available. Still widely documented and used, though being superseded by `nftables`. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-A|Append a rule to a chain|
|-I|Insert a rule (at a specifc positon)|
|-D|Delete a rule|
|-L -n -v|List rules, numeric, verbose|
|-p tcp/udp|Protocol|
|--dport / --sport|Destnaton / source port|
|-j ACCEPT/DROP/REJECT|Acton to take|



Page 63 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Real-World Example:** 

```
sudo iptables -L -n -v --line-numbers
```

**CAUTION — Production Risk:** Changing firewall rules on a remote production machine over SSH can lock you out instantly if you accidentally block your own connection (e.g. a default DROP policy applied before an ACCEPT rule for your IP/SSH port exists). Always add the allow-rule for your own access first, test in a second session before closing the first, and consider a scheduled rule-rollback safety net. 

###### **`iptables-save / iptables-restore`** 

Dumps the current ruleset to a text file (for backup/version control) or loads one back in bulk. 

```
sudo iptables-save > /etc/iptables/rules.v4
sudo iptables-restore < /etc/iptables/rules.v4
```

###### **`nft`** 

The modern replacement for iptables/ip6tables/arptables/ebtables, unifying them under one syntax and one kernel subsystem (nftables). New deployments should generally target `nft` over legacy `iptables`. 

```
sudo nft list ruleset
```

```
sudo nft add rule inet filter input tcp dport 22 accept
```

#### **18.1 Legacy vs Modern** 

||**iptables (legacy)**|**nfables / nf (modern)**|
|---|---|---|
|Status|Stll widely deployed, in maintenance mode on<br>many distros|Default backend on current<br>Debian/RHEL/Fedora releases|
|Syntax|One command per protocol family (iptables,<br>ip6tables...)|Single unifed syntax for IPv4/IPv6|
|Performance|Linear rule evaluaton|More efcient rule-set evaluaton|
|Recommendaton|Know it — stll common in documentaton and<br>older systems|Prefer for new systems where available|



Page 64 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **19. tcpdump — Detailed Section** 

##### **`tcpdump`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Captures and displays raw network packets traversing an interface — the deepest level of network troubleshooting short of a full packet-capture GUI (Wireshark). 

###### **Syntax:** 

```
tcpdump [options] [filter expression]
```

###### **Example:** 

```
sudo tcpdump -i eth0 port 443
```

**Explanation:** Filters combine protocol, host, port, and direction (`src`/`dst`) expressions. `-nn` disables both hostname and port-name resolution (faster, and shows raw numbers). `-w` writes a capture to a file for later analysis (e.g. in Wireshark); `-r` reads one back. 

**DevOps Use Case:** Confirming whether expected traffic is actually arriving at/leaving a host, diagnosing TCP handshake failures, verifying a firewall/security-group change took effect, capturing evidence during an active incident. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-i any / eth0|Interface to capture on|
|-nn|Don't resolve hostnames or port names|
|port 80/443|Filter by port|
|host 10.0.0.10|Filter by host (either directon)|
|src host / dst host|Filter by source or destnaton only|
|-w fle.pcap|Write capture to a fle|
|-r fle.pcap|Read from a capture fle|
|-c N|Capture N packets then stop|



###### **Real-World Example:** 

```
sudo tcpdump -i any -nn port 80
sudo tcpdump -i eth0 host 10.0.0.10 and port 443
sudo tcpdump -i eth0 -w capture.pcap -c 500
tcpdump -r capture.pcap
```

**CAUTION — Production Risk:** Capturing on a busy production interface can itself add load and generate very large files quickly — always scope filters tightly (specific host/port) and use `-c` to cap the packet count. 

###### Common capture recipes: 

```
sudo tcpdump -i any                     # everything, all interfaces
sudo tcpdump -i eth0                    # everything on eth0
```

Page 65 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
sudo tcpdump port 80                    # HTTP traffic
sudo tcpdump port 443                   # HTTPS traffic
sudo tcpdump host 10.0.0.10             # traffic to/from a specific host
sudo tcpdump src host 10.0.0.10         # traffic FROM a host
sudo tcpdump dst host 10.0.0.10         # traffic TO a host
sudo tcpdump -nn 'tcp[tcpflags] & (tcp-syn) != 0'   # SYN packets only
```

Page 66 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **20. nmap** 

**CAUTION — Production Risk:** Only scan hosts and networks you own or have explicit written authorization to test. Scanning third-party systems without permission may violate laws such as the U.S. Computer Fraud and Abuse Act and equivalent legislation elsewhere. 

##### **`nmap`** 

**Purpose:** Network exploration and security auditing tool for host discovery, port scanning, and service/version detection. 

###### **Syntax:** 

```
nmap [options] target
```

###### **Example:** 

```
nmap 10.0.1.5
```

**Explanation:** A bare `nmap <host>` scans the 1,000 most common TCP ports. `-p` restricts to specific ports. `-sV` probes open ports to identify the running service and version. 

**DevOps Use Case:** Verifying which ports are actually reachable on a server you manage before/after a firewall change, auditing your own infrastructure for unintentionally exposed services. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-p 80,443|Scan specifc ports|
|-p-|Scan all 65535 ports|
|-sV|Detect service/version on open ports|
|-sS|SYN ('stealth') scan — needs root|
|-A|Aggressive: OS detecton, version detecton, traceroute|
|-Pn|Skip host-discovery ping (scan even if host doesn't answer ICMP)|



###### **Real-World Example:** 

```
nmap -p 80,443 10.0.1.5
nmap -sV 10.0.1.5
```

**Note:** Only run against systems you are authorized to test. 

Page 67 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **21. Network Troubleshooting** 

A repeatable methodology beats guessing. Work outward from the local machine toward the destination: local config → DNS → routing → firewall/security groups → load balancer → server → application. 

#### **Scenario 1 — Server Cannot Reach the Internet** 

```
ip addr           # does the interface have an IP address?
ip route          # is there a default route/gateway?
ping -c 3 <gateway-ip>     # can we reach the gateway at all?
ping -c 3 8.8.8.8          # can we reach the internet by IP (rules out DNS)?
dig example.com            # does DNS resolve?
curl -v https://example.com  # does an actual HTTP request succeed?
traceroute 8.8.8.8         # where does the path break?
```

#### **Scenario 2 — Application Not Reachable on Port 8080** 

```
sudo ss -lntp | grep 8080     # is anything even listening?
sudo lsof -i :8080            # which process, confirm it's the right one
curl localhost:8080           # does it respond locally on the server itself?
curl <server-ip>:8080         # does it respond from outside the server?
# if local works but remote doesn't -> check firewall/security group rules
```

#### **Scenario 3 — DNS Is Not Working** 

```
cat /etc/resolv.conf     # which DNS servers is this host configured to use?
resolvectl status        # effective DNS servers per interface (systemd-resolved)
dig example.com          # does resolution work at all?
dig @8.8.8.8 example.com # does it work against a known-good public resolver?
nslookup example.com     # cross-check with a second tool
```

#### **Scenario 4 — High Network Latency** 

```
ping -c 20 <target>       # baseline latency and packet loss
mtr <target>              # live per-hop latency/loss over time
traceroute <target>       # identify which hop introduces the delay
ss -ti                    # inspect TCP internals (retransmits, RTT) for active
connections
```

#### **Scenario 5 — Connection Timeout: A Layered Checklist** 

Work through the request path in order, confirming each hop before moving to the next: 

19. Client — is the client itself configured correctly (proxy settings, local firewall)? 

20. DNS — does the hostname resolve to the expected IP? (`dig`) 

21. Routing — is there a valid path from client to destination network? (`traceroute`/`mtr`) 

22. Firewall / Security Group — does a rule allow this specific port/protocol/source? (`iptables -L`, cloud security group console/CLI) 

23. Load Balancer — is the LB healthy, and are backend targets passing health checks? (cloud console, `curl` the LB directly) 

Page 68 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

24. Server — is the server up and is the service actually listening? (`ss -lntp`) 

25. Application — is the application itself healthy, or hung/overloaded? (application logs, `curl localhost:<port>` on the server itself) 

Page 69 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **22. Git Commands for DevOps** 

Git underpins every modern CI/CD pipeline. DevOps engineers need more than the basics — rebasing, bisecting, and reflog recovery are regular tools of the trade. 

#### **22.1 Core Workflow** 

```
git init                      # create a new repository
git clone <url>                # copy a remote repository locally
git status                     # show changed/staged/untracked files
git add file.txt                # stage a file
git add -A                     # stage all changes
git commit -m "message"        # commit staged changes
git push origin main            # push commits to remote
git pull origin main            # fetch + merge from remote
git fetch                      # download remote changes without merging
```

###### **`git branch`** 

Lists, creates, or deletes branches. 

```
git branch
git branch feature/new-api
git branch -d old-branch
```

###### **`git switch`** 

Switches to another branch (modern, safer replacement for `checkout` when changing branches). 

```
git switch main
git switch -c feature/x   # create and switch
```

###### **`git checkout`** 

Legacy multi-purpose command — switches branches or restores files from a commit. Still very common, but `switch`/`restore` split its responsibilities more safely. 

```
git checkout feature/x
git checkout -- file.txt   # discard local changes to a file
```

##### **`git merge`** 

**Purpose:** Integrates changes from one branch into another, creating a merge commit if histories have diverged. **Syntax:** 

```
git merge <branch>
```

###### **Example:** 

```
git checkout main && git merge feature/x
```

**Explanation:** Preserves the full history of both branches. Conflicts must be resolved manually if the same lines were changed differently on both sides. 

**DevOps Use Case:** Merging a completed feature branch into main/develop as part of a PR/MR workflow. **Real-World Example:** 

```
git merge --no-ff feature/x
```

Page 70 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**Note:** `--no-ff` forces a merge commit even when a fast-forward is possible, preserving a clear record that a feature branch existed — often required by team conventions. 

##### **`git rebase`** 

**Purpose:** Replays commits from one branch onto another, producing a linear history instead of a merge commit. **Syntax:** 

```
git rebase <branch>
```

###### **Example:** 

```
git checkout feature/x && git rebase main
```

**Explanation:** Rewrites commit history (new commit hashes) — useful for keeping a feature branch up to date with main before merging, and for cleaning up commit history with `git rebase -i`. 

**DevOps Use Case:** Keeping a long-lived feature branch current without merge-commit noise; squashing/reordering commits before opening a pull request. 

###### **Real-World Example:** 

```
git rebase -i HEAD~5   # interactive rebase, last 5 commits
```

**CAUTION — Production Risk:** Never rebase commits that have already been pushed and are in use by others, unless the whole team agrees — it rewrites history and force-pushing can silently discard others' work. 

###### **`git log`** 

Shows commit history. 

```
git log --oneline --graph --all
git log -p -- file.txt
```

###### **`git diff`** 

Shows changes between commits, working directory, and the staging area. 

```
git diff
git diff --staged
git diff main..feature/x
```

###### **`git stash`** 

Temporarily shelves uncommitted changes so you can switch context, then reapply them later. 

```
git stash
git stash pop
git stash list
```

##### **`git reset`** 

**Purpose:** Moves the current branch pointer, optionally altering the staging area and working directory. 

###### **Syntax:** 

```
git reset [--soft|--mixed|--hard] <commit>
```

**Example:** 

Page 71 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
git reset --soft HEAD~1
```

**Explanation:** `--soft` keeps changes staged, `--mixed` (default) unstages but keeps changes in the working directory, `--hard` discards changes entirely. 

**DevOps Use Case:** Undoing a local commit before pushing, or discarding an experimental change entirely. 

###### **Real-World Example:** 

```
git reset --hard origin/main   # discard ALL local changes, match remote exactly
```

**CAUTION — Production Risk:** `git reset --hard` permanently discards uncommitted work in the working directory — there's no undo beyond `git reflog` recovery for already-committed states. 

###### **`git revert`** 

Creates a new commit that undoes a previous commit's changes, without rewriting history. The safe way to undo changes that are already pushed/shared. 

```
git revert <commit-hash>
```

###### **`git cherry-pick`** 

Applies a specific commit from one branch onto another. 

```
git cherry-pick <commit-hash>
```

_Tip: Common for backporting a hotfix from main into a release branch._ 

###### **`git tag`** 

Marks a specific commit, typically for releases. 

```
git tag v1.4.0
git push origin v1.4.0
```

###### **`git remote`** 

Manages remote repository references. 

```
git remote -v
git remote add origin <url>
```

##### **`git reflog`** 

**Purpose:** Shows a log of every place HEAD has pointed — including commits no longer reachable from any branch. 

###### **Syntax:** 

```
git reflog
```

###### **Example:** 

```
git reflog
```

**Explanation:** Git rarely truly deletes data immediately; reflog is the safety net after a bad `reset --hard`, an accidental branch deletion, or a botched rebase. 

**DevOps Use Case:** Recovering 'lost' commits after a destructive operation — a genuine incident-recovery tool, not just a curiosity. 

###### **Real-World Example:** 

Page 72 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
git reflog
git reset --hard HEAD@{2}   # restore to a prior state shown in reflog
```

###### **`git bisect`** 

Binary-searches commit history to find which commit introduced a bug, by marking commits good/bad. 

```
git bisect start
git bisect bad
git bisect good v1.0.0
```

Typical CI/CD-relevant Git workflow: 

```
git clone <repo-url>
git checkout -b feature/payment-retry
# ...make changes...
git add -A && git commit -m "Add retry logic for payment gateway"
git push origin feature/payment-retry
# open PR/MR -> CI runs tests -> review -> merge
git tag v2.3.0 && git push origin v2.3.0   # triggers a release pipeline
```

Page 73 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **23. Docker Commands** 

#### **23.1 Core Concepts** 

|**Concept**|**Meaning**|
|---|---|
|Image|An immutable, layered flesystem + metadata template used to create containers|
|Container|A running (or stopped) instance of an image, isolated via namespaces/cgroups|
|Dockerfle|A build script defning how to create an image|
|Volume|Persistent storage that outlives a container's lifecycle|
|Network|A virtual network connectng containers to each other and/or the host|
|Registry|A storage/distributon service for images (Docker Hub, ECR, GCR, ACR, private registries)|



###### **`docker version / docker info`** 

Shows client/server version info and daemon-wide configuration/resource summary. 

```
docker version
docker info
```

###### **`docker pull`** 

Downloads an image from a registry. 

```
docker pull nginx:1.27
```

###### **`docker images`** 

Lists locally stored images. 

```
docker images
```

##### **`docker build`** 

**Purpose:** Builds an image from a Dockerfile. 

###### **Syntax:** 

```
docker build [options] -t name:tag context
```

###### **Example:** 

```
docker build -t myapp:1.0 .
```

**Explanation:** `-t` tags the resulting image; the trailing `.` is the build context (files sent to the daemon, respecting .dockerignore). `--no-cache` forces a full rebuild ignoring layer cache. 

**DevOps Use Case:** The core step in every containerized CI/CD pipeline — producing the deployable artifact. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-t name:tag|Tag the image|
|-f path|Use a Dockerfle at a non-default path|
|--no-cache|Ignore build cache|



Page 74 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|--build-arg|Pass a build-tme variable|



###### **Real-World Example:** 

```
docker build -t registry.example.com/myapp:$(git rev-parse --short HEAD) .
```

##### **`docker run`** 

**Purpose:** Creates and starts a new container from an image. 

###### **Syntax:** 

```
docker run [options] image [command]
```

###### **Example:** 

```
docker run -d -p 8080:80 --name web nginx
```

**Explanation:** `-d` detached (background), `-p host:container` maps ports, `--name` sets a container name, `-e` sets an environment variable, `-v` mounts a volume, `--rm` auto-removes the container on exit. 

**DevOps Use Case:** Starting an application container locally or on a server; testing an image before deploying it to an orchestrator. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-d|Detached (background)|
|-p host:container|Publish a port|
|-e KEY=val|Set environment variable|
|-v host:container|Mount a volume/bind mount|
|--name|Assign a container name|
|--rm|Remove container automatcally on exit|
|--restart=policy|Restart policy (no, on-failure, always, unless-stopped)|



###### **Real-World Example:** 

```
docker run -d --name api -p 3000:3000 -e NODE_ENV=production --restart unless-
stopped myapp:1.0
```

###### **`docker ps`** 

Lists running containers (`-a` includes stopped ones). 

```
docker ps
docker ps -a
```

###### **`docker stop / start / restart`** 

Controls a container's running state — `stop` sends SIGTERM then SIGKILL after a grace period. 

Page 75 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
docker stop web
docker start web
docker restart web
```

##### **`docker rm / docker rmi`** 

**Purpose:** `docker rm` removes a stopped container; `docker rmi` removes an image. 

###### **Syntax:** 

```
docker rm [options] container
docker rmi [options] image
```

###### **Example:** 

```
docker rm web
docker rmi myapp:old
```

**Explanation:** `docker rm -f` force-removes a running container (stops it first). An image can't be removed while a container (even a stopped one) still references it. 

**DevOps Use Case:** Cleaning up old containers/images to reclaim disk space, especially on CI build agents. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-f|Force removal|
|-v (rm)|Also remove associated anonymous volumes|



###### **Real-World Example:** 

```
docker rm -f $(docker ps -aq --filter status=exited)
```

**Note:** `docker rmi` on an image still used by a running container will fail (as intended) — stop/remove dependent containers first. 

##### **`docker exec`** 

**Purpose:** Runs a command inside an already-running container. 

###### **Syntax:** 

`docker exec [options] container command` **Example:** `docker exec -it web /bin/sh` 

**Explanation:** `-it` allocates an interactive TTY — needed for an interactive shell session. Without `-it`, useful for oneoff diagnostic commands. 

**DevOps Use Case:** Getting a shell inside a running container to inspect files, check environment variables, or run a debugging command without restarting it. 

**Common Options:** 

Page 76 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Opton**|**Meaning**|
|---|---|
|-it|Interactve TTY|
|-u user|Run as a specifc user|
|-w dir|Set working directory|



###### **Real-World Example:** 

```
docker exec -it web sh -c "cat /etc/nginx/nginx.conf"
```

##### **`docker logs`** 

**Purpose:** Shows a container's stdout/stderr output. 

###### **Syntax:** 

```
docker logs [options] container
```

**Example:** 

```
docker logs -f web
```

**Explanation:** `-f` follows in real time (like `tail -f`); `--tail N` shows only the last N lines; `--since` filters by time. **DevOps Use Case:** The first command to run when a container is crash-looping or behaving unexpectedly. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-f|Follow live|
|--tail N|Show last N lines|
|--since|Time flter|
|-t|Show tmestamps|



###### **Real-World Example:** 

```
docker logs --tail 100 -f web
```

###### **`docker inspect`** 

Dumps full low-level JSON metadata about a container/image/network/volume — IP address, mounts, env vars, restart count, exit code. 

```
docker inspect web
docker inspect -f '{{.State.ExitCode}}' web
```

###### **`docker cp`** 

Copies files between a container and the host filesystem. 

```
docker cp web:/var/log/app.log ./app.log
```

###### **`docker network`** 

Page 77 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

Manages Docker networks, connecting containers to each other. 

```
docker network ls
docker network create app-net
docker network connect app-net web
```

###### **`docker volume`** 

Manages named volumes for persistent container data. 

```
docker volume ls
docker volume create app-data
docker volume inspect app-data
```

##### **`docker system`** 

**Purpose:** Manages and reports on overall Docker resource usage. 

###### **Syntax:** 

```
docker system [command]
```

###### **Example:** 

```
docker system prune -a
```

**Explanation:** `prune` removes unused containers, networks, images, and (with `--volumes`) volumes to reclaim disk space. `df` shows disk usage by category. 

**DevOps Use Case:** Regular cleanup on build agents and hosts where accumulated stopped containers/dangling images fill up disk space. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|prune|Remove unused data|
|prune -a|Also remove unused (not just dangling) images|
|df|Show Docker disk usage|



###### **Real-World Example:** 

```
docker system df
docker system prune -af --volumes
```

**CAUTION — Production Risk:** `docker system prune -af --volumes` is destructive — it removes ALL unused images and volumes, including ones you may want to keep for rollback. Review `docker system df` first. 

###### **`docker stats`** 

Live streaming view of CPU, memory, network, and I/O usage per container — the `top` of Docker. 

```
docker stats
```

###### **`docker tag / docker push / docker login`** 

`tag` labels an image (often for a registry path), `push` uploads it, `login` authenticates to a registry. 

```
docker tag myapp:1.0 registry.example.com/myapp:1.0
```

Page 78 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
docker login registry.example.com
docker push registry.example.com/myapp:1.0
```

Page 79 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **24. Docker Compose** 

Docker Compose defines and runs multi-container applications from a single `docker-compose.yml` file — the standard way to run local dev environments that mirror production topology (app + database + cache, etc.). 

```
docker compose up -d           # start all services, detached
docker compose down            # stop and remove containers, networks
docker compose ps              # list running services
docker compose logs -f web     # follow logs for a specific service
docker compose exec web sh     # shell into a running service
docker compose build           # build/rebuild images defined in the file
docker compose restart web     # restart a single service
docker compose pull            # pull latest images for all services
```

**Note:** `docker compose down -v` also removes named volumes — that means database data in a local dev stack. Omit `- v` unless you specifically want to wipe persisted data. 

Page 80 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **25. Kubernetes Commands** 

kubectl is the primary interface to a Kubernetes cluster. This section covers the commands used daily for deploying, inspecting, and troubleshooting workloads. 

##### **`kubectl get`** 

**Purpose:** Lists resources of a given type. 

###### **Syntax:** 

```
kubectl get <resource> [name] [options]
```

###### **Example:** 

```
kubectl get pods
```

**Explanation:** `-o wide` adds extra columns (node, IP); `-o yaml`/`-o json` dumps full resource definitions; `-n namespace` scopes to a namespace; `--all-namespaces`/`-A` spans all namespaces; `-w` watches for changes live. 

**DevOps Use Case:** The default 'what's the current state of my cluster' command — pods, deployments, services, nodes, and more. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-o wide|Extra columns (node, IP)|
|-o yaml / -o json|Full resource defniton|
|-n namespace|Scope to a namespace|
|-A|All namespaces|
|-w|Watch for live changes|
|-l key=value|Filter by label selector|



###### **Real-World Example:** 

```
kubectl get pods -n production -o wide
kubectl get pods -l app=api -w
```

##### **`kubectl describe`** 

**Purpose:** Shows detailed information about a resource, including recent events — often the single most useful troubleshooting command in Kubernetes. 

###### **Syntax:** 

```
kubectl describe <resource> <name>
```

###### **Example:** 

```
kubectl describe pod <pod-name>
```

**Explanation:** The Events section at the bottom reveals scheduling failures, image pull errors, readiness/liveness probe failures, and OOM kills. 

Page 81 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**DevOps Use Case:** The second step (after `get`) in almost every Kubernetes troubleshooting session — explains *why* a pod is Pending, CrashLooping, or not receiving traffic. 

###### **Real-World Example:** 

```
kubectl describe pod my-app-7d4f9c-xk2p9
```

##### **`kubectl logs`** 

**Purpose:** Retrieves container logs from a pod. 

###### **Syntax:** 

```
kubectl logs [options] pod
```

###### **Example:** 

```
kubectl logs <pod-name>
```

**Explanation:** `-f` follows live; `--previous` shows logs from the last crashed instance of a container — essential for CrashLoopBackOff diagnosis (the current container may not have started long enough to log anything useful). `-c` selects a container in a multi-container pod. 

**DevOps Use Case:** The primary tool for diagnosing application-level failures inside a pod. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-f|Follow live|
|--tail=N|Last N lines|
|--previous|Logs from the previous (crashed) container instance|
|-c container|Specifc container in a mult-container pod|



###### **Real-World Example:** 

```
kubectl logs my-app-7d4f9c-xk2p9 -f --tail=100
kubectl logs my-app-7d4f9c-xk2p9 --previous
```

##### **`kubectl exec`** 

**Purpose:** Runs a command inside a running container in a pod. 

###### **Syntax:** 

```
kubectl exec [-it] pod -- command
```

###### **Example:** 

```
kubectl exec -it <pod-name> -- /bin/sh
```

**Explanation:** Mirrors `docker exec`. Use `-c container` to target a specific container in a multi-container pod. 

**DevOps Use Case:** Interactive debugging inside a live pod — checking environment variables, testing connectivity to a dependent service, inspecting mounted config. 

**Real-World Example:** 

Page 82 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
kubectl exec -it my-app-7d4f9c-xk2p9 -- curl localhost:8080/health
```

##### **`kubectl apply`** 

**Purpose:** Creates or updates resources declaratively from a YAML/JSON manifest, reconciling the cluster state to match the file. 

###### **Syntax:** 

```
kubectl apply -f file.yaml
```

###### **Example:** 

```
kubectl apply -f deployment.yaml
```

**Explanation:** The standard way to deploy — idempotent, and diffable against the live state. `-f -` reads from stdin, common when piping generated manifests from a templating tool. 

**DevOps Use Case:** The core deploy command in nearly every Kubernetes CI/CD pipeline. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-f fle.yaml|Apply a manifest fle|
|-f dir/|Apply all manifests in a directory|
|--dry-run=client|Preview without applying|



###### **Real-World Example:** 

```
kubectl apply -f k8s/ --dry-run=client
kubectl apply -f k8s/
```

###### **`kubectl create / kubectl delete`** 

`create` imperatively creates a resource (fails if it already exists); `delete` removes a resource by name or manifest. 

```
kubectl create namespace staging
kubectl delete pod <pod-name>
kubectl delete -f deployment.yaml
```

###### **`kubectl edit`** 

Opens a live resource in your editor for direct modification, applying changes on save. 

```
kubectl edit deployment my-app
```

_Tip: Prefer `apply -f` from version-controlled manifests over `edit` for anything meant to be reproducible/auditable._ 

##### **`kubectl rollout`** 

**Purpose:** Manages the rollout lifecycle of Deployments/StatefulSets/DaemonSets — status, history, and rollback. 

###### **Syntax:** 

```
kubectl rollout <command> deployment/<name>
```

**Example:** 

Page 83 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### `kubectl rollout status deployment/my-app` 

**Explanation:** `status` watches a rollout until it completes or fails; `undo` rolls back to the previous (or a specified `-to-revision`) version; `history` lists past revisions. 

**DevOps Use Case:** Watching a deployment progress in CI/CD, and rolling back instantly if a bad release causes errors. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|status|Watch rollout progress|
|undo|Roll back to previous revision|
|undo --to-revision=N|Roll back to a specifc revision|
|history|List revision history|



###### **Real-World Example:** 

```
kubectl rollout status deployment/my-app
kubectl rollout undo deployment/my-app
```

###### **`kubectl scale`** 

Changes the replica count of a Deployment/StatefulSet/ReplicaSet. 

```
kubectl scale deployment my-app --replicas=5
```

###### **`kubectl expose`** 

Creates a Service exposing an existing resource (Deployment/Pod) to the network. 

```
kubectl expose deployment my-app --port=80 --target-port=8080 --type=ClusterIP
```

##### **`kubectl port-forward`** 

**Purpose:** Forwards a local port to a port on a pod/service, without needing an Ingress or NodePort. 

###### **Syntax:** 

```
kubectl port-forward pod local:remote
```

###### **Example:** 

```
kubectl port-forward my-app-7d4f9c-xk2p9 8080:8080
```

**Explanation:** Traffic to localhost:8080 on your machine tunnels through the Kubernetes API server to the target port on the pod. 

**DevOps Use Case:** Quickly accessing a database, admin UI, or internal service running in-cluster for local debugging, without exposing it publicly. 

###### **Real-World Example:** 

```
kubectl port-forward svc/my-app 8080:80
```

###### **`kubectl config`** 

Manages kubeconfig contexts — which cluster/namespace/user kubectl currently targets. 

Page 84 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
kubectl config get-contexts
kubectl config use-context prod-cluster
kubectl config set-context --current --namespace=staging
```

_Tip: Always double check `kubectl config current-context` before running destructive commands — running `kubectl delete` against the wrong cluster context is a classic incident cause._ 

###### **`kubectl top`** 

Shows live CPU/memory usage for nodes or pods (requires the metrics-server add-on). 

```
kubectl top nodes
kubectl top pods -n production
```

###### **`kubectl explain`** 

Shows the documentation and field structure for a resource type/field, directly from the API — faster than searching docs. 

```
kubectl explain deployment.spec.template.spec.containers
```

#### **25.1 Common Diagnostic Commands** 

```
kubectl get pods
kubectl get pods -o wide
kubectl describe pod <pod>
kubectl logs <pod>
kubectl logs <pod> -f
kubectl exec -it <pod> -- /bin/sh
kubectl get svc
kubectl get deployments
kubectl get endpoints
kubectl get events --sort-by=.lastTimestamp
kubectl rollout status deployment/<name>
kubectl rollout undo deployment/<name>
```

#### **25.2 Kubernetes Troubleshooting Chain** 

When a workload isn't working end to end, trace the request path: Pod → Deployment → Service → Ingress → DNS → Network. 

26. Pod — is it Running and Ready? `kubectl get pods` then `kubectl describe pod` for events, `kubectl logs` for app errors. 

27. Deployment — does it have the desired replica count available? `kubectl get deployment` / `kubectl rollout status`. 

28. Service — does it have endpoints pointing at healthy pods? `kubectl get endpoints <service>` — an empty list means the Service's selector doesn't match any Ready pod. 

29. Ingress — is the Ingress resource correctly routing to the Service, and is the Ingress controller healthy? `kubectl describe ingress`. 

30. DNS — can pods resolve internal service names? `kubectl exec -it <pod> -- nslookup my-service`. 

31. Network — are NetworkPolicies or security groups blocking traffic between pods/nodes? Review NetworkPolicy resources and cloud-level firewall rules. 

Page 85 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **26. Cloud CLI Commands** 

#### **26.1 AWS CLI** 

###### **`aws configure`** 

Sets up credentials, default region, and output format for the AWS CLI. 

```
aws configure
aws configure --profile prod
```

###### **`aws sts`** 

Security Token Service — used to verify identity and assume roles. 

```
aws sts get-caller-identity
```

_Tip: The fastest way to confirm which AWS account/role your current credentials actually resolve to before running anything destructive._ 

###### **`aws ec2`** 

Manages EC2 instances, security groups, volumes, and networking. 

```
aws ec2 describe-instances --filters "Name=tag:Name,Values=web-*"
aws ec2 start-instances --instance-ids i-0123456789
aws ec2 describe-security-groups --group-ids sg-0123456789
```

###### **`aws s3`** 

Manages S3 buckets and objects — a common target for storing build artifacts, backups, and static assets. 

```
aws s3 ls s3://my-bucket/
aws s3 cp build.tar.gz s3://my-bucket/releases/
aws s3 sync ./dist s3://my-bucket/static/
```

###### **`aws iam`** 

Manages users, roles, and policies for access control. 

```
aws iam list-roles
aws iam get-role --role-name deploy-role
```

###### **`aws eks`** 

Manages Elastic Kubernetes Service clusters. 

```
aws eks update-kubeconfig --name prod-cluster --region us-east-1
aws eks describe-cluster --name prod-cluster
```

_Tip: `update-kubeconfig` is the standard first step to point `kubectl` at an EKS cluster._ 

###### **`aws logs`** 

Reads/manages CloudWatch Logs. 

```
aws logs tail /ecs/my-app --follow
aws logs describe-log-groups
```

#### **26.2 Azure CLI** 

###### **`az login`** 

Authenticates the Azure CLI, opening a browser (or device-code flow) to sign in. 

Page 86 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
az login
```

###### **`az account`** 

Manages which subscription commands target. 

```
az account list
az account set --subscription "Prod Subscription"
```

###### **`az vm`** 

Manages virtual machines. 

```
az vm list -o table
az vm start --name web01 --resource-group prod-rg
az vm restart --name web01 --resource-group prod-rg
```

###### **`az storage`** 

Manages storage accounts, blobs, and file shares. 

```
az storage blob upload --account-name mystorage --container-name releases --file
build.tar.gz
```

###### **`az network`** 

Manages virtual networks, NSGs (network security groups), load balancers. 

```
az network nsg rule list --nsg-name prod-nsg --resource-group prod-rg -o table
```

###### **`az aks`** 

Manages Azure Kubernetes Service clusters. 

```
az aks get-credentials --name prod-cluster --resource-group prod-rg
```

#### **26.3 Google Cloud CLI** 

###### **`gcloud auth`** 

Authenticates the gcloud CLI. 

```
gcloud auth login
gcloud auth application-default login
```

###### **`gcloud config`** 

Manages active project, region, and account configuration. 

```
gcloud config set project my-project-id
gcloud config list
```

###### **`gcloud compute`** 

Manages Compute Engine VMs, firewall rules, and networking. 

```
gcloud compute instances list
gcloud compute instances reset web-01 --zone=us-central1-a
```

###### **`gcloud storage`** 

Manages Cloud Storage buckets and objects (modern replacement for `gsutil` for most operations). 

```
gcloud storage cp build.tar.gz gs://my-bucket/releases/
```

Page 87 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **`gcloud container`** 

Manages Google Kubernetes Engine (GKE) clusters. 

```
gcloud container clusters get-credentials prod-cluster --zone us-central1-a
```

**Note:** Across all three clouds, the very first step in any session should be confirming identity/context (`aws sts getcaller-identity`, `az account show`, `gcloud config list`) — running the right command against the wrong account/subscription/project is a common and costly mistake. 

Page 88 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **27. Terraform CLI** 

Terraform's core workflow — init, validate, plan, apply — maps directly onto how Infrastructure as Code changes should move through review and deployment. 

###### **`terraform init`** 

Initializes a working directory: downloads providers/modules and configures the backend. 

```
terraform init
```

_Tip: Run again after adding a new provider/module or changing the backend configuration._ 

###### **`terraform validate`** 

Checks configuration syntax and internal consistency without touching real infrastructure. 

```
terraform validate
```

###### **`terraform fmt`** 

Rewrites .tf files into canonical formatting — run in pre-commit hooks/CI to keep style consistent. 

```
terraform fmt -recursive
```

##### **`terraform plan`** 

**Purpose:** Computes and displays the changes Terraform would make to reach the desired state, without applying them. 

###### **Syntax:** 

```
terraform plan [options]
```

###### **Example:** 

```
terraform plan -out=tfplan
```

**Explanation:** Shows resources to be created (+), updated (~), or destroyed (-). `-out` saves the plan to a file that `apply` can execute exactly, avoiding drift between plan and apply. 

**DevOps Use Case:** The mandatory review step before any infrastructure change — reviewed in a pull request or CI pipeline before anyone runs `apply`. 

###### **Real-World Example:** 

```
terraform plan -out=tfplan -var-file=prod.tfvars
```

##### **`terraform apply`** 

**Purpose:** Applies the planned changes, creating/updating/destroying real infrastructure. 

###### **Syntax:** 

```
terraform apply [plan-file]
```

###### **Example:** 

```
terraform apply tfplan
```

**Explanation:** Without a saved plan file, `apply` computes a fresh plan and prompts for confirmation before proceeding. 

Page 89 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**DevOps Use Case:** The step that actually provisions infrastructure — should always be preceded by a reviewed `plan`, especially in production. 

###### **Real-World Example:** 

```
terraform apply tfplan
```

**CAUTION — Production Risk:** Never run `terraform apply` with `-auto-approve` against production without a reviewed plan — it's the single most common cause of accidental infrastructure destruction. 

##### **`terraform destroy`** 

**Purpose:** Destroys all resources managed by the current Terraform state. 

###### **Syntax:** 

```
terraform destroy
```

###### **Example:** 

```
terraform destroy
```

**Explanation:** Effectively the inverse of `apply` — tears down everything Terraform knows about in the current workspace/state. 

**DevOps Use Case:** Tearing down temporary/ephemeral environments (e.g. a PR preview environment); rarely intended for production. 

**CAUTION — Production Risk:** Extremely destructive — always confirm the correct workspace/state and target with `terraform workspace show` / `terraform state list` before running this against anything shared. 

###### **`terraform state`** 

Inspects and manipulates the Terraform state file directly (list, show, move, remove resources from tracking). 

```
terraform state list
terraform state show aws_instance.web
terraform state rm aws_instance.old
```

_Tip: `state rm` removes a resource from Terraform's tracking without destroying the real infrastructure — useful for adopting unmanaged resources or splitting state files carefully._ 

###### **`terraform show`** 

Displays the current state or a saved plan in human-readable form. 

```
terraform show tfplan
```

###### **`terraform output`** 

Prints output values defined in the configuration (e.g. a resulting IP address or ARN), useful for chaining into scripts. 

```
terraform output
terraform output -raw vpc_id
```

###### **`terraform import`** 

Brings an existing, manually-created resource under Terraform management by associating it with a resource block. 

```
terraform import aws_instance.web i-0123456789
```

###### **`terraform workspace`** 

Page 90 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

Manages multiple named state files from a single configuration (e.g. dev/staging/prod). 

```
terraform workspace list
terraform workspace new staging
terraform workspace select prod
```

Where each command fits in the IaC workflow: 

```
terraform init        # once per checkout / after adding providers
terraform fmt -recursive && terraform validate   # local sanity checks
terraform plan -out=tfplan     # reviewed in PR/CI
terraform apply tfplan         # applied after approval
```

Page 91 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **28. Ansible Commands** 

|**Concept**|**Meaning**|
|---|---|
|Inventory|A list of managed hosts, optonally grouped (statc fle or dynamic script/plugin)|
|Playbook|A YAML fle defning a sequence of tasks/plays to run against hosts|
|Role|A reusable, structured bundle of tasks, templates, and variables|
|Handler|A task that only runs when notfed by another task (e.g. restart a service afer a confg<br>change)|
|Idempotency|Running the same playbook repeatedly produces the same end state without unintended<br>side efects|
|Vault|Ansible's built-in mechanism for encryptng sensitve variables/fles at rest|



##### **`ansible`** 

**Purpose:** Runs a single ad-hoc module/command against a set of hosts, without writing a full playbook. 

###### **Syntax:** 

```
ansible <host-pattern> -m module -a arguments
```

###### **Example:** 

```
ansible webservers -m ping
```

**Explanation:** `-m` selects the module (e.g. `shell`, `ping`, `copy`, `service`); `-a` passes module arguments; `-i` specifies the inventory. 

**DevOps Use Case:** Quick one-off tasks across a fleet — checking connectivity, restarting a service everywhere, or gathering facts — without the overhead of a playbook. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-m module|Module to run|
|-a args|Module arguments|
|-i inventory|Inventory fle/source|
|-b|Become (sudo)|
|--limit|Restrict to a subset of hosts|



###### **Real-World Example:** 

```
ansible webservers -i inventory.ini -m service -a "name=nginx state=restarted" -b
```

##### **`ansible-playbook`** 

**Purpose:** Executes a playbook — the primary way Ansible automation is actually run in production. 

**Syntax:** 

Page 92 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
ansible-playbook [options] playbook.yml
```

###### **Example:** 

```
ansible-playbook -i inventory.ini site.yml
```

**Explanation:** `--check` performs a dry run without making changes; `--diff` shows what would change; `--limit` restricts execution to specific hosts/groups; `-e` passes extra variables. 

**DevOps Use Case:** Applying configuration, deploying application code, patching servers — the core automation execution command. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-i inventory|Inventory source|
|--check|Dry run|
|--dif|Show fle difs for changes|
|--limit host|Restrict to specifc hosts|
|-e "var=value"|Pass extra variables|
|--tags|Run only tasks with matching tags|



###### **Real-World Example:** 

```
ansible-playbook -i inventory.ini deploy.yml --limit webservers --check --diff
```

**Note:** Always run with `--check --diff` against production first to preview changes before a real run, especially for unfamiliar playbooks. 

###### **`ansible-inventory`** 

Inspects and validates inventory data (static or dynamic). 

```
ansible-inventory -i inventory.ini --list
```

###### **`ansible-galaxy`** 

Installs and manages roles/collections from Ansible Galaxy or Git sources. 

```
ansible-galaxy install geerlingguy.docker
ansible-galaxy collection install amazon.aws
```

##### **`ansible-vault`** 

**Purpose:** Encrypts and decrypts sensitive files/variables so secrets can be safely committed to version control. 

**Syntax:** 

```
ansible-vault [command] file
```

###### **Example:** 

```
ansible-vault encrypt secrets.yml
```

Page 93 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**Explanation:** `encrypt`/`decrypt` operate on whole files; `view` shows decrypted content without writing it to disk; `edit` opens an encrypted file for editing in place. **DevOps Use Case:** Storing database passwords, API keys, and TLS private keys inside a playbook repository safely. **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|encrypt|Encrypt a fle|
|decrypt|Decrypt a fle|
|view|View decrypted content without saving|
|edit|Edit an encrypted fle in place|
|--ask-vault-pass|Prompt for the vault password|



###### **Real-World Example:** 

```
ansible-vault view secrets.yml --vault-password-file=.vault_pass
```

Page 94 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **29. CI/CD Commands** 

CI/CD platforms (Jenkins, GitHub Actions, GitLab CI/CD, Argo CD) orchestrate the same underlying Linux, Git, Docker, Kubernetes, and cloud CLI commands covered throughout this handbook. Understanding the platform-specific YAML/DSL matters less than understanding what's actually executing under the hood. 

A typical build-and-deploy pipeline sequence: 

```
# 1. Checkout
git clone <repo-url> && cd repo
# 2. Build
docker build -t registry.example.com/myapp:$(git rev-parse --short HEAD) .
```

```
# 3. Test (example)
docker run --rm registry.example.com/myapp:$(git rev-parse --short HEAD) npm test
# 4. Tag & Push
docker tag registry.example.com/myapp:$(git rev-parse --short HEAD)
registry.example.com/myapp:latest
docker push registry.example.com/myapp:$(git rev-parse --short HEAD)
docker push registry.example.com/myapp:latest
```

```
# 5. Deploy
```

```
kubectl set image deployment/myapp myapp=registry.example.com/myapp:$(git rev-parse
--short HEAD)
kubectl rollout status deployment/myapp
```

#### **29.1 Platform Notes** 

|**Platorm**|**What it's really doing**|
|---|---|
|Jenkins|Runs a Groovy-defned Jenkinsfle as a series of shell steps on an agent — usually just the<br>commands above, wrapped in `sh '...'` blocks|
|GitHub Actons|YAML workfow with `steps:` that run shell commands or reusable 'actons' (many of which<br>are thin wrappers around the CLI tools in this handbook)|
|GitLab CI/CD|YAML `.gitlab-ci.yml` with `script:` blocks executed inside a runner container — same<br>shell/Docker/kubectl commands underneath|
|Argo CD|GitOps contnuous delivery for Kubernetes — watches a Git repo of manifests and<br>reconciles the cluster to match, rather than a pipeline pushing changes directly with<br>`kubectl apply`|



**Note:** Argo CD inverts the traditional 'push' deploy model: instead of a pipeline running `kubectl apply`, Argo CD continuously pulls the desired state from Git and reconciles the cluster to match it (GitOps). 

Page 95 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **30. Monitoring and Performance Commands** 

Most of these tools were introduced earlier for their primary purpose; this section groups them by the performance question they answer. 

|**Queston**|**Commands**|
|---|---|
|High CPU — who, and how much?|top, htop, mpstat, pidstat|
|High memory — who, and how much?|free -h, top (sort by %MEM), ps aux --sort=-%mem|
|Disk I/O botleneck?|iostat -x 2, vmstat 2, sar -d|
|Network throughput/errors?|ss -s, ip -s link, sar -n DEV|
|Overall load trend?|uptme, sar (historical), vmstat|
|What is a process actually doing?|strace -p <pid>, lsof -p <pid>|



###### **`iostat`** 

Reports CPU and per-device I/O statistics — util%, await (latency), throughput. Part of the `sysstat` package. 

```
iostat -x 2 5
```

_Tip: A device consistently near 100% `%util` with high `await` indicates disk I/O is the bottleneck._ 

###### **`sar`** 

Collects and reports historical system activity (CPU, memory, disk, network) from data gathered over time — invaluable for 'what happened at 3am' investigations. Part of `sysstat`. 

```
sar -u 2 5     # CPU
sar -r 2 5     # memory
sar -n DEV 2 5 # network
```

###### **`mpstat`** 

Per-CPU-core utilization breakdown — reveals whether load is spread evenly or pinned to one core (common with singlethreaded bottlenecks). 

```
mpstat -P ALL 2 5
```

###### **`pidstat`** 

Per-process CPU, memory, and I/O statistics over time (like `top`, but scriptable/loggable snapshots). 

```
pidstat -p <pid> 2 5
```

##### **`strace`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Traces system calls and signals made by a process — the deepest level of 'what is this process actually doing right now'. 

###### **Syntax:** 

```
strace [options] -p pid
```

**Example:** 

Page 96 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
strace -p 1234
```

**Explanation:** `-c` summarizes syscall counts/time instead of a live stream; `-e trace=network` filters to specific syscall categories; attaching to a live process requires appropriate permissions (root, or same-user with ptrace allowed). 

**DevOps Use Case:** Diagnosing why a process is hanging (stuck on a specific syscall like a blocking read/connect), which files it's trying (and failing) to open, or measuring syscall-level overhead. 

###### **Common Options:** 

|**Opton**|**Meaning**|
|---|---|
|-p pid|Atach to a running process|
|-c|Summary of syscall counts/tme|
|-e trace=|Filter to a syscall category (network, fle, ...)|
|-f|Follow forked child processes|



###### **Real-World Example:** 

```
strace -f -e trace=network -p $(pgrep -f myapp)
```

**CAUTION — Production Risk:** `strace` adds significant overhead to the traced process — use briefly and with a specific hypothesis in production, not as a first blind step. 

Page 97 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **31. Advanced Linux Commands** 

###### **`nsenter`** 

Enters the namespaces of another process (network, mount, PID, etc.) — commonly used to debug a container from the host by attaching to its namespaces directly. 

```
sudo nsenter -t <pid> -n ss -tulpn
```

_Tip: Extremely useful for inspecting a container's network stack without needing tools installed inside a minimal/distroless container image._ 

###### **`chroot`** 

Runs a command with a different apparent root directory, isolating its filesystem view. 

```
sudo chroot /mnt/recovery /bin/bash
```

_Tip: Used in rescue-boot recovery scenarios and lightweight filesystem isolation — not a security sandbox on its own._ 

###### **`unshare`** 

Runs a command in new namespaces (mount, PID, network, etc.) without a container runtime — the low-level primitive containers are built on. 

```
sudo unshare --net bash
```

###### **`sysctl`** 

Views and sets kernel runtime parameters. 

```
sysctl net.ipv4.ip_forward
sudo sysctl -w net.core.somaxconn=1024
sysctl -a | grep net.ipv4
```

_Tip: Persist changes in /etc/sysctl.conf or /etc/sysctl.d/ — `sysctl -w` changes are lost on reboot._ 

###### **`ulimit`** 

Views/sets per-shell resource limits (open files, processes, core dump size) — a common cause of 'too many open files' errors under `ulimit -n`. 

```
ulimit -a
ulimit -n 65536
```

###### **`ethtool`** 

Queries/configures network interface driver and hardware settings (link speed, duplex, offload features). 

```
ethtool eth0
```

##### **`perf`** 

**Note:** This command typically requires `sudo` / root privileges. 

**Purpose:** Linux's built-in performance profiling toolkit, sampling CPU usage down to function/call-stack level. **Syntax:** 

```
perf [command] [options]
```

###### **Example:** 

```
sudo perf top
```

Page 98 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

**Explanation:** `perf top` shows a live, function-level view of where CPU time is going system-wide; `perf record`/`perf report` capture a profile for offline analysis. 

**DevOps Use Case:** Root-causing CPU-bound performance problems at the code level when `top` only tells you which process, not which function. 

###### **Real-World Example:** 

```
sudo perf record -p <pid> -g -- sleep 30 && sudo perf report
```

**Note:** Requires kernel perf_events support and appropriate privileges; profiling overhead is generally low but should still be scoped and time-boxed in production. 

Quick reference for when to reach for each advanced tool: 

|**Command**|**Use when**|
|---|---|
|strace|You need to see exactly which syscalls a stuck/misbehaving process is making|
|lsof|You need to know what fles/sockets a process has open|
|tcpdump|You need to see actual packets on the wire|
|nmap|You need to verify which ports are reachable on a host you own|
|nsenter|You need to inspect a container's namespace from the host|
|chroot / unshare|You need flesystem or namespace isolaton for recovery or low-level testng|
|sysctl / ulimit|You're tuning kernel or per-process resource limits|
|perf|You need functon-level CPU profling, not just process-level|



Page 99 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **32. DevOps Troubleshooting Playbooks** 

Each playbook follows the same structure: Symptoms → Possible Causes → Commands to Run → What It Tells Us → Interpretation → Fixes → Verification. Use these as a repeatable checklist during an incident rather than improvising from scratch. 

#### **32.1 Server Down** 

###### **Symptoms:** 

- Server unreachable via SSH, monitoring shows it as down 

###### **Possible Causes:** 

- Instance crashed or was terminated 

- Kernel panic 

- Network/security group misconfiguration 

- Disk full preventing normal operation 

- Provider-side outage 

###### **Commands to Run:** 

```
ping <server-ip>
ssh -v user@<server-ip>
# from cloud console: check instance status/system log
# check cloud provider status page
```

###### **Interpreting the Output:** 

- No ping response + no SSH: likely fully down or network-blocked, not just an app issue. 

- SSH times out but ping works: SSH service or firewall issue, not a full outage. 

###### **Possible Fixes:** 

- Restart/reboot the instance from the cloud console if unresponsive. 

- Check the console's serial/system log for boot errors. 

- Restore from backup/snapshot if the disk is corrupted. 

###### **Verification:** 

- Confirm ping and SSH both succeed. 

- Confirm core services report `active` via systemctl. 

- Confirm the application responds on its expected port. 

#### **32.2 Website Down** 

###### **Symptoms:** 

- Users report the site is unreachable or shows a connection error 

###### **Possible Causes:** 

- Web server process crashed 

- DNS misconfiguration 

- TLS certificate expired 

- Load balancer has no healthy targets 

- Upstream/application server down 

###### **Commands to Run:** 

Page 100 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
curl -Iv https://example.com
dig example.com
systemctl status nginx
ss -lntp | grep 443
curl -v https://example.com 2>&1 | grep -i expire
```

###### **Interpreting the Output:** 

- Connection refused: nothing listening, service is likely down. 

- DNS resolves to the wrong/old IP: DNS or CDN issue. 

- TLS handshake error mentioning expiry: certificate problem. 

###### **Possible Fixes:** 

- Restart the web server: systemctl restart nginx. 

- Renew the TLS certificate if expired. 

- Check and fix DNS records if pointing to a stale IP. 

- Check load balancer target health in the cloud console. 

###### **Verification:** 

- curl returns 200 with correct content. 

- TLS certificate valid and not near expiry. 

- DNS resolves to the correct current IP. 

#### **32.3 API Returning 500** 

###### **Symptoms:** 

- Clients receive HTTP 500 Internal Server Error responses 

###### **Possible Causes:** 

- Unhandled application exception 

- Database connection failure 

- Downstream dependency (cache, queue, third-party API) unavailable 

- Misconfigured environment variable after a deploy 

###### **Commands to Run:** 

```
journalctl -u myapp --since "10 minutes ago"
kubectl logs <pod> --tail=200
curl -v https://api.example.com/health
systemctl status postgresql
```

###### **Interpreting the Output:** 

- Stack trace in logs points to the exact failing component. 

- 'Connection refused' to DB/cache in logs points to a dependency outage, not app code. 

- Errors starting right after a deploy timestamp strongly suggest the new release is the cause. 

###### **Possible Fixes:** 

- Roll back the last deployment if errors correlate with it (kubectl rollout undo). 

- Restart the failing dependency if it's down. 

- Fix and redeploy if it's a genuine code/config bug. 

###### **Verification:** 

- Error rate returns to baseline in logs/metrics. 

- curl against the endpoint returns 200 with expected payload. 

Page 101 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **32.4 Port Not Listening** 

###### **Symptoms:** 

- Application unreachable on its expected port 

###### **Possible Causes:** 

- Service crashed on startup 

- Service bound to the wrong interface (127.0.0.1 instead of 0.0.0.0) 

- Port already in use by another process 

- Firewall blocking the port 

###### **Commands to Run:** 

```
sudo ss -lntp | grep <port>
sudo lsof -i :<port>
journalctl -u myapp -n 50
sudo iptables -L -n | grep <port>
```

###### **Interpreting the Output:** 

- No output from ss/lsof: the service isn't running or crashed on startup — check logs. 

- Listening on 127.0.0.1 only: won't accept external connections — needs to bind to 0.0.0.0. 

- Another process already owns the port: 'address already in use' error explained. 

###### **Possible Fixes:** 

- Fix the bind address in app config. 

- Stop the conflicting process, or change the app's port. 

- Restart the service and re-check ss output. 

- Add a firewall rule if the port is blocked. 

###### **Verification:** 

- ss -lntp shows the expected process listening on the correct interface/port. 

- curl localhost:<port> succeeds locally, then curl <server-ip>:<port> succeeds remotely. 

#### **32.5 DNS Failure** 

###### **Symptoms:** 

- Hostnames fail to resolve; application can't reach dependencies by name 

###### **Possible Causes:** 

- Wrong nameservers configured 

- DNS record deleted or misconfigured 

- DNS provider outage 

- Stale/cached negative response 

###### **Commands to Run:** 

```
cat /etc/resolv.conf
resolvectl status
dig example.com
dig @8.8.8.8 example.com
```

###### **Interpreting the Output:** 

- Resolution fails against local resolver but succeeds against 8.8.8.8: local DNS server/config issue. 

Page 102 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

- Resolution fails against every resolver: the record itself is missing/wrong at the authoritative nameserver. 

###### **Possible Fixes:** 

- Fix /etc/resolv.conf or the DHCP/DNS config supplying it. 

- Correct the DNS record at the registrar/DNS provider. 

- Flush local DNS cache if a stale negative result is suspected. 

###### **Verification:** 

- dig returns the correct, expected IP consistently from multiple resolvers. 

#### **32.6 SSL/TLS Certificate Problem** 

###### **Symptoms:** 

- Browser/clients show certificate warnings or TLS handshake failures 

###### **Possible Causes:** 

- Certificate expired 

- Certificate doesn't match the hostname (SAN mismatch) 

- Incomplete certificate chain (missing intermediate cert) 

- Clock skew on the server 

###### **Commands to Run:** 

```
curl -vI https://example.com 2>&1 | grep -i -A2 certificate
openssl s_client -connect example.com:443 -servername example.com
date
```

###### **Interpreting the Output:** 

- 'certificate has expired' — renewal overdue. 

- 'unable to get local issuer certificate' — intermediate chain isn't being served. 

- Hostname mismatch error — SAN/CN doesn't include the requested domain. 

###### **Possible Fixes:** 

- Renew the certificate (e.g. via certbot / ACME client) and reload the web server. 

- Ensure the full chain (leaf + intermediates) is configured, not just the leaf cert. 

- Correct server clock via NTP if skewed. 

###### **Verification:** 

- openssl s_client shows 'Verify return code: 0 (ok)'. 

- curl succeeds without -k. 

#### **32.7 High CPU** 

###### **Symptoms:** 

- Server or container CPU usage sustained near 100% 

###### **Possible Causes:** 

- Runaway process/infinite loop 

- Traffic spike beyond capacity 

- Inefficient code path (e.g. missing index causing full table scans) 

- Cryptomining malware (rare but real) 

###### **Commands to Run:** 

Page 103 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
top / htop
ps aux --sort=-%cpu | head
top -H -p <pid>
journalctl -u myapp --since "30 minutes ago"
```

###### **Interpreting the Output:** 

- One process dominates CPU: identify and investigate that specific process/service. 

- Many processes evenly high: likely genuine load beyond current capacity, consider scaling. 

- Unrecognized process consuming CPU: investigate for compromise. 

###### **Possible Fixes:** 

- Restart the offending service to restore availability. 

- Scale horizontally/vertically if it's genuine load. 

- Optimize the identified slow code path. 

- If compromise is suspected, isolate the host and engage incident response. 

###### **Verification:** 

- CPU usage returns to normal baseline in top/monitoring. 

- Application latency/error rate back to normal. 

#### **32.8 High Memory** 

###### **Symptoms:** 

- Server or container memory usage climbing toward the limit; possible OOM kills 

###### **Possible Causes:** 

- Memory leak in the application 

- Undersized memory limit for actual workload 

- Excessive caching without eviction 

- A dependent process consuming unexpected memory 

###### **Commands to Run:** 

###### `free -h` 

```
ps aux --sort=-%mem | head
dmesg -T | grep -i "out of memory"
kubectl top pods (if on Kubernetes)
```

###### **Interpreting the Output:** 

- 'available' memory near zero and swap heavily used: real memory pressure. 

- dmesg shows 'Killed process': confirms the OOM killer already intervened. 

- Steady upward memory trend over hours/days without traffic change: likely a leak. 

###### **Possible Fixes:** 

- Restart the affected process/pod to reclaim memory immediately. 

- Increase memory limits if the workload genuinely needs more. 

- Investigate and fix the leak (heap dump/profiler for the specific language runtime). 

- Adjust cache eviction policy if caching is the cause. 

###### **Verification:** 

- free -h / kubectl top shows stable, healthy memory usage over time. 

- No new OOM-kill entries in dmesg/journalctl. 

Page 104 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **32.9 Disk Full** 

###### **Symptoms:** 

- 'No space left on device' errors; services failing to write logs or data 

###### **Possible Causes:** 

- Unbounded log growth 

- Old backups/artifacts never cleaned up 

- A large deleted-but-still-open file (see df vs du in Chapter 6) 

- Genuine data growth outpacing provisioned disk 

###### **Commands to Run:** 

```
df -h
du -sh /var/* | sort -rh | head
lsof | grep deleted
find / -xdev -size +500M -exec ls -lh {} \;
```

###### **Interpreting the Output:** 

- df shows 100% on a specific mount: that's the filesystem to investigate. 

- du doesn't add up to df's used space: check for deleted-but-open files via lsof. 

- One directory (e.g. /var/log) dominates usage: rotate/clean logs there. 

###### **Possible Fixes:** 

- Clear old logs (respecting retention needs) or force logrotate. 

- Restart a process still holding a deleted file open, releasing that space. 

- Expand the volume/disk if growth is legitimate and expected. 

- Move old backups/artifacts to cheaper long-term storage (e.g. S3) and remove locally. 

###### **Verification:** 

- df -h shows healthy free space margin. 

- Services writing logs/data successfully again. 

#### **32.10 Inode Exhaustion** 

###### **Symptoms:** 

- 'No space left on device' even though df shows free disk space 

###### **Possible Causes:** 

- Enormous number of small files (e.g. session files, cache files, mail queue) exhausting the inode table 

###### **Commands to Run:** 

```
df -i
find / -xdev -printf '%h\n' | sort | uniq -c | sort -rn | head
```

###### **Interpreting the Output:** 

- df -i shows IUse% near 100% while df -h shows plenty of free space: classic inode exhaustion signature. 

- A single directory tree accounts for the vast majority of files: that's the source. 

###### **Possible Fixes:** 

- Delete/archive the excess small files (e.g. old session/cache files). 

- Reconfigure the offending application to clean up after itself (TTL/cleanup job). 

- As a last resort, reformat with a filesystem/inode ratio suited to the workload (destructive — requires backup/restore). 

Page 105 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Verification:** 

- df -i shows healthy free inode count. 

- Application can create new files successfully again. 

#### **32.11 Slow Application** 

###### **Symptoms:** 

- Response times elevated; users report sluggishness without full outage 

###### **Possible Causes:** 

- Database query performance degradation 

- Insufficient CPU/memory/IO capacity for current load 

- Network latency to a dependency 

- Garbage collection pauses (managed-runtime languages) 

###### **Commands to Run:** 

```
top / vmstat 2
iostat -x 2
ss -ti  (check retransmits/RTT on active connections)
Application-level slow-query log / APM traces
```

###### **Interpreting the Output:** 

- High iowait in vmstat/top: disk I/O bound, check iostat for the specific device. 

- High CPU with normal I/O: compute bound, profile the hot code path. 

- Normal local resource usage but slow anyway: likely a slow downstream dependency — check APM traces. 

###### **Possible Fixes:** 

- Add/optimize database indexes for slow queries. 

- Scale resources (CPU/memory/IOPS) matching the bottleneck identified. 

- Cache expensive, repeatable operations. 

- Tune GC settings or investigate memory pressure causing frequent collection. 

###### **Verification:** 

- Latency/response-time percentiles (p50/p95/p99) return to baseline. 

#### **32.12 Network Latency** 

###### **Symptoms:** 

- Elevated round-trip time between hosts or to an external dependency 

###### **Possible Causes:** 

- Congested network path/hop 

- Undersized instance with network throttling 

- Cross-region traffic taking a suboptimal path 

- MTU mismatch causing fragmentation 

###### **Commands to Run:** 

```
ping -c 20 <target>
mtr <target>
traceroute <target>
```

Page 106 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Interpreting the Output:** 

- Latency increases consistently at one specific hop in mtr: that hop/link is the bottleneck. 

- Latency is fine locally but high to a specific external service: likely path/provider-side, not your infrastructure. 

###### **Possible Fixes:** 

- Move the dependent service closer (same region/AZ) if cross-region latency is the cause. 

- Contact the network/cloud provider if the issue is at a hop outside your control. 

- Adjust MTU settings if fragmentation is suspected. 

###### **Verification:** 

- mtr/ping shows latency back within expected bounds. 

#### **32.13 Packet Loss** 

###### **Symptoms:** 

- Intermittent connection drops, retransmissions, or timeouts 

###### **Possible Causes:** 

- Network congestion 

- Faulty hardware/NIC on the path 

- Security device (firewall/IPS) dropping packets under load 

- Wireless/last-mile issues (less common in datacenter/cloud) 

###### **Commands to Run:** 

###### `mtr -rw -c 200 <target>` 

```
ip -s link  (check RX/TX error and drop counters on the interface)
ss -ti  (check retransmit counts on active TCP sessions)
```

###### **Interpreting the Output:** 

- Loss concentrated at one hop across many mtr samples: that hop is dropping packets. 

- Rising RX/TX error counters on the local interface: local NIC/driver issue. 

###### **Possible Fixes:** 

- Escalate to network/cloud provider if loss is on an upstream hop outside your control. 

- Replace/reset the NIC or driver if local interface errors are climbing. 

- Reduce load or scale bandwidth if congestion is self-inflicted. 

###### **Verification:** 

- mtr shows 0% (or baseline-normal) loss across all hops sustained over time. 

#### **32.14 Docker Container Crashing** 

###### **Symptoms:** 

- Container repeatedly exits shortly after starting 

###### **Possible Causes:** 

- Application error on startup (bad config, missing env var) 

- Out-of-memory kill (container memory limit too low) 

- Missing dependency inside the image 

- Incorrect CMD/ENTRYPOINT 

###### **Commands to Run:** 

Page 107 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
docker ps -a
docker logs <container>
docker inspect <container> -f '{{.State.ExitCode}} {{.State.OOMKilled}}'
```

###### **Interpreting the Output:** 

- Exit code 1 with an app stack trace in logs: application-level bug/misconfiguration. 

- OOMKilled: true: container memory limit is too low for the workload. 

- Exit code 127: command not found — image/entrypoint misconfiguration. 

###### **Possible Fixes:** 

- Fix the identified config/env var and rebuild/redeploy. 

- Raise the container memory limit if legitimately OOM-killed. 

- Correct the Dockerfile ENTRYPOINT/CMD if it's referencing a missing binary/script. 

###### **Verification:** 

- docker ps shows the container Up and stable (not restarting) over several minutes. 

- docker logs shows normal startup output with no repeated crash loop. 

#### **32.15 Kubernetes Pod CrashLoopBackOff** 

###### **Symptoms:** 

- Pod repeatedly restarts; status shows CrashLoopBackOff 

###### **Possible Causes:** 

- Application crashes on startup (bug, bad config, missing secret/configmap) 

- Failing liveness probe killing an otherwise-healthy pod prematurely 

- Insufficient resources causing OOM kill 

###### **Commands to Run:** 

```
kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod> --previous
kubectl get events --sort-by=.lastTimestamp
```

###### **Interpreting the Output:** 

- describe shows 'Back-off restarting failed container' plus a recent OOMKilled reason: resource limit issue. 

- logs --previous shows an application stack trace: app-level bug/config problem. 

- Liveness probe failing in Events but the app logs look healthy: the probe itself (timeout/path) may be misconfigured. 

###### **Possible Fixes:** 

- Fix the underlying application error revealed in --previous logs. 

- Increase memory/CPU requests-limits if OOMKilled. 

- Adjust liveness probe timing/thresholds if it's killing a slow-starting but otherwise healthy app. 

- Verify required ConfigMaps/Secrets are mounted correctly. 

###### **Verification:** 

- kubectl get pods shows Running and Ready with a stable (non-incrementing) restart count. 

#### **32.16 Kubernetes ImagePullBackOff** 

###### **Symptoms:** 

Page 108 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

- Pod stuck in ImagePullBackOff / ErrImagePull status 

###### **Possible Causes:** 

- Wrong image name or tag 

- Private registry requires authentication that isn't configured (missing imagePullSecrets) 

- Registry unreachable from the cluster (network/firewall) 

- Rate limiting from the registry 

###### **Commands to Run:** 

```
kubectl describe pod <pod>
kubectl get events --sort-by=.lastTimestamp
```

###### **Interpreting the Output:** 

- 'manifest not found' / 'not found': the image name or tag is wrong or was never pushed. 

- 'unauthorized' / 'authentication required': missing or invalid imagePullSecrets. 

- Timeout reaching the registry: network/firewall/DNS issue from the node. 

###### **Possible Fixes:** 

- Correct the image name/tag in the manifest and reapply. 

- Create/attach the correct imagePullSecrets for private registries. 

- Verify node-to-registry network path (DNS, firewall, proxy config). 

###### **Verification:** 

- kubectl describe pod shows the image pulled successfully and the container Running. 

#### **32.17 Kubernetes Service Not Reachable** 

###### **Symptoms:** 

- Requests to a Service time out or connection-refuse, even though pods appear healthy 

###### **Possible Causes:** 

- Service selector doesn't match pod labels 

- No pods are Ready (failing readiness probes) 

- NetworkPolicy blocking traffic 

- Wrong targetPort configured on the Service 

###### **Commands to Run:** 

```
kubectl get endpoints <service>
kubectl describe svc <service>
kubectl get pods -l <selector> -o wide
kubectl exec -it <pod> -- curl localhost:<targetPort>
```

###### **Interpreting the Output:** 

- Endpoints list is empty: the Service selector matches no Ready pod — check labels and readiness probes. 

- Endpoints list is populated but requests still fail: likely a NetworkPolicy or targetPort mismatch. 

###### **Possible Fixes:** 

- Fix mismatched labels between the Service selector and pod template. 

- Fix a failing readiness probe so pods become Ready and get added as endpoints. 

- Correct the Service's targetPort to match the container's actual listening port. 

- Review NetworkPolicy resources for unintended blocking rules. 

###### **Verification:** 

- kubectl get endpoints shows healthy pod IPs. 

Page 109 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

- A test request through the Service succeeds. 

#### **32.18 CI/CD Pipeline Failure** 

###### **Symptoms:** 

- A pipeline run fails at build, test, or deploy stage 

###### **Possible Causes:** 

- Flaky/failing test 

- Missing or expired credentials/secrets for a step 

- Dependency/registry unavailable 

- Environment drift between CI runner and target environment 

###### **Commands to Run:** 

```
# review the pipeline's stage logs directly in the CI platform UI
git log -1 --stat   # confirm what actually changed in this run
docker build -t test-local . (reproduce a build failure locally)
```

###### **Interpreting the Output:** 

- Failure only in the deploy stage, build/test passed: likely a credentials or target-environment issue, not the code change itself. 

- Same failure reproduces locally: a genuine code/config bug, not a CI environment quirk. 

###### **Possible Fixes:** 

- Rotate/update expired credentials in the CI platform's secret store. 

- Fix the failing test or mark it as legitimately quarantined with a tracked follow-up. 

- Pin dependency versions if an upstream registry change caused the break. 

###### **Verification:** 

- Pipeline runs green end to end on the next commit/retry. 

#### **32.19 SSH Connection Failure** 

###### **Symptoms:** 

- Cannot SSH into a server — connection refused, timeout, or authentication failure 

###### **Possible Causes:** 

- sshd not running 

- Firewall/security group blocking port 22 (or custom SSH port) 

- Wrong key or key not authorized on the server 

- Account locked or disabled 

###### **Commands to Run:** 

```
ssh -v user@<server-ip>
nc -zv <server-ip> 22
# from the server console (if reachable another way): systemctl status sshd
```

###### **Interpreting the Output:** 

- 'Connection refused': sshd isn't running, or the wrong port is being used. 

- Connection hangs/times out: firewall/security group is blocking the port. 

- 'Permission denied (publickey)': the key isn't authorized, or the wrong key/user is being used. 

Page 110 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

###### **Possible Fixes:** 

- Start sshd if stopped: systemctl start sshd (via console access if SSH itself is down). 

- Open the port in the firewall/security group for the source IP. 

- Add the correct public key to ~/.ssh/authorized_keys via console/rescue access. 

###### **Verification:** 

- ssh -v shows a successful connection and shell prompt. 

Page 111 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **33. Real-World DevOps Command Workflows** 

#### **33.1 Investigating a Production Server** 

```
uptime                # load average and how long it's been up
top                    # live CPU/memory snapshot
free -h                # memory summary
df -h                  # disk space per filesystem
df -i                  # inode usage
ss -tulpn              # listening ports and owning processes
systemctl --failed     # any failed services?
journalctl -p err -b   # error-level logs since boot
```

Each command answers a different layer of 'is this box healthy': `uptime`/`top`/`free` cover compute, `df` covers storage, `ss` covers networking, and `systemctl --failed` / `journalctl` cover service-level health. Running them in this order builds a complete picture in under a minute. 

#### **33.2 Investigating a Web Server** 

```
ss -lntp                          # confirm the web server is listening
curl -I localhost                 # does it respond locally?
curl -v https://example.com       # does it respond from outside, with valid TLS?
tail -f /var/log/nginx/error.log  # watch for errors live
```

#### **33.3 Investigating a Docker Container** 

```
docker ps                         # is it running?
docker logs <container>           # what is it saying?
docker inspect <container>        # full config, mounts, env, restart count
docker stats                      # live resource usage
docker exec -it <container> /bin/sh   # get inside and look around
```

#### **33.4 Investigating Kubernetes** 

```
kubectl get pods                  # overall pod status
kubectl describe pod <pod>        # events — why is it in this state?
kubectl logs <pod>                # application-level output
kubectl get svc                   # is the Service defined correctly?
kubectl get endpoints             # does the Service have healthy backends?
kubectl get events --sort-by=.lastTimestamp   # cluster-wide recent events
```

This sequence walks outward from the pod itself (is the container even running and healthy) to the Service layer (is traffic actually being routed to it) — the same Pod → Service troubleshooting chain introduced in Chapter 25. 

Page 112 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **34. Command Comparison Tables** 

|**Command**|**Purpose**||**When to**|**Use**|
|---|---|---|---|---|
|ps|Process snapshot||One-tm|e investgaton, scriptng|
|top|Live process monit|oring|Interact<br>troubles|ve CPU/memory<br>hootng|
|htop|Interactve process|monitor|Interact<br>sortng/|ve investgaton with<br>fltering|
|**grep vs awk vs sed**|**grep**|**awk**||**sed**|
|Purpose|Find matching lines|Extract/process col<br>generate reports|umns,|Transform text, fnd-and-<br>replace|
|Best for|'Does this patern exist, and<br>where?'|'Give me feld 3 wh<br>9 equals 500'|ere feld|'Replace X with Y across this<br>fle'|
|Typical use|grep -i error app.log|awk '{print $1,$4}'<br>access.log||sed 's/foo/bar/g' fle.txt|



#### **grep vs awk vs sed** 

#### **curl vs wget** 

||**curl**|**wget**|
|---|---|---|
|Best for|API testng, arbitrary HTTP methods|Downloading and saving fles|
|Default output|stdout|saves to disk|



#### **scp vs rsync** 

||**scp**|**rsync**|
|---|---|---|
|Transfers|Whole fles, every tme|Only the diferences (delta transfer)|
|Resume support|No|Yes|
|Best for|Quick one-of copies|Repeated syncs, large directories,<br>backups|



#### **df vs du** 

||**df**|**du**|
|---|---|---|
|Reports|Filesystem-level space usage|Directory/fle-level space usage|



Page 113 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

||**df**|**du**|
|---|---|---|
|Source of truth|Kernel/flesystem block accountng|Walking the visible directory tree|
|Can disagree because|Deleted-but-open fles stll count in<br>df, not in du|—|



#### **ss vs netstat** 

||**ss**|**netstat**|
|---|---|---|
|Status|Modern, actvely maintained|Legacy, deprecated in net-tools|
|Performance|Faster on systems with many sockets|Slower at scale|
|Recommendaton|Preferred default|Know it for older docs/scripts|



#### **systemctl vs service** 

||**systemctl**|**service**|
|---|---|---|
|System|systemd (modern distros)|SysV init / upstart (legacy, or a<br>compatbility shim)|
|Capabilites|Full unit management, dependencies,<br>logs via journalctl|Basic start/stop/restart/status only|



#### **iptables vs nftables** 

||**iptables (legacy)**|**nfables (modern)**|
|---|---|---|
|Syntax|Per-protocol-family commands|Unifed syntax for IPv4/IPv6|
|Status on new distros|Ofen a compatbility shim over<br>nfables|Natve default backend|



#### **apt vs dnf** 

||**apt (Debian/Ubuntu)**|**dnf (RHEL/Fedora)**|
|---|---|---|
|Package format|.deb|.rpm|
|Update index|apt update|dnf check-update|
|Install|apt install pkg|dnf install pkg|



Page 114 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **docker vs kubectl** 

||**docker**|**kubectl**|
|---|---|---|
|Scope|Single host/daemon, individual<br>containers|A cluster of nodes, orchestratng<br>many containers|
|Unit of work|Container|Pod (and higher-level<br>Deployment/Service/etc.)|
|Best for|Local development, building images|Producton orchestraton, scaling,<br>self-healing|



Page 115 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **35. Top 100 Commands Every DevOps Engineer Should Know** 

Ranked roughly by how often they're needed in real DevOps/SRE work. 'Difficulty' reflects how much background knowledge is needed to use the command safely and effectively, not how complex the syntax looks. 

|**Command**|**Category**|**Difculty**|**What It Does**|**Key**<br>**Opton**|**DevOps Use Case**|
|---|---|---|---|---|---|
|ls|Files|Beginner|List directory contents|-la|Verify deployed fles exist|
|cd|Navigaton|Beginner|Change directory|-|Navigate server flesystem|
|pwd|Navigaton|Beginner|Print working directory|-P|Confrm script locaton|
|cat|Files|Beginner|Print fle contents|-|Quick fle inspecton|
|grep|Search|Beginner|Search text for a patern|-i, -r|Find errors in logs|
|fnd|Search|Beginner|Search flesystem by criteria|-name, -<br>mtme|Clean up old fles|
|chmod|Permissions|Beginner|Change fle permissions|+x, 755|Make scripts executable|
|chown|Permissions|Beginner|Change fle ownership|-R|Fix app fle ownership|
|cp / mv / rm|Files|Beginner|Copy / move / delete|-r, -f|Backups, cleanup|
|tail|Logs|Beginner|View end of a fle|-f|Live-tail logs|
|head|Logs|Beginner|View start of a fle|-n|Inspect log headers|
|less|Logs|Beginner|Page through a fle|/patern|Browse large logs|
|ps|Process|Beginner|Snapshot of processes|aux|Investgate running<br>processes|
|top / htop|Process|Beginner|Live process monitor|M, P|Diagnose CPU/memory<br>issues|
|kill|Process|Beginner|Send a signal to a process|-9|Stop a stuck process|
|df|Storage|Beginner|Disk space usage|-h, -i|Diagnose disk-full errors|
|du|Storage|Beginner|Directory size usage|-sh|Find what's using disk<br>space|
|tar|Archiving|Beginner|Archive/compress fles|-czvf|Package releases/backups|
|ssh|Remote|Beginner|Remote shell access|-i, -J|Access remote servers|
|scp / rsync|Remote|Beginner|Copy fles over SSH|-r, -avz|Deploy fles, backups|
|sudo|Privilege|Beginner|Run as another user|-u|Privileged operatons|
|systemctl|Services|Beginner|Manage systemd services|status,<br>restart|Control app services|
|journalctl|Logs|Beginner|Query systemd logs|-u, -f|Read service logs|
|ping|Network|Beginner|Test host reachability|-c|Quick connectvity check|
|ip addr / ip|Network|Beginner|View IPs and routes|-|Inspect networking confg|



Page 116 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Command**|**Category**|**Difculty**|**What It Does**|**Key**<br>**Opton**|**DevOps Use Case**|
|---|---|---|---|---|---|
|route||||||
|curl|Network|Beginner|HTTP requests from CLI|-I, -v, -X|Test APIs and health<br>checks|
|wget|Network|Beginner|Download fles|-O|Fetch release artfacts|
|dig|DNS|Beginner|DNS lookups|+short|Diagnose DNS issues|
|ss|Network|Beginner|Socket/port statstcs|-tulpn|Check listening ports|
|lsof|Network/<br>Process|Intermedi<br>ate|List open fles/sockets|-i :port|Find process on a port|
|awk|Text|Intermedi<br>ate|Column/report text<br>processing|-F|Parse structured logs|
|sed|Text|Intermedi<br>ate|Stream text editor|-i, s///g|Bulk confg edits|
|xargs|Text|Intermedi<br>ate|Build commands from input|-I{}|Bulk operatons|
|sort / uniq|Text|Beginner|Sort and dedupe lines|-n, -c|Analyze log frequency|
|cron / crontab|Scheduling|Intermedi<br>ate|Schedule recurring jobs|-e, -l|Automate maintenance<br>tasks|
|nohup|Process|Intermedi<br>ate|Run immune to hangups|&|Long-running background<br>jobs|
|watch|Process|Beginner|Repeat a command live|-n|Monitor changing output|
|strace|Advanced|Advanced|Trace syscalls|-p, -c|Deep process diagnostcs|
|tcpdump|Network|Advanced|Packet capture|-i, -w|Deep network diagnostcs|
|nmap|Network|Advanced|Port/service scanning|-p, -sV|Audit open ports (own<br>systems)|
|iptables / nf|Firewall|Advanced|Packet fltering rules|-L, -A|Manage frewall rules|
|mtr /<br>traceroute|Network|Intermedi<br>ate|Path/latency diagnostcs|-|Diagnose latency/loss|
|nslookup / host|DNS|Beginner|DNS lookups|-|Quick DNS check|
|nc|Network|Intermedi<br>ate|Raw TCP/UDP tool|-zv|Test port reachability|
|useradd /<br>usermod|Users|Intermedi<br>ate|Manage user accounts|-m, -aG|Provision service accounts|
|passwd|Users|Beginner|Manage passwords|-l|Lock/reset accounts|
|free|System|Beginner|Memory usage|-h|Diagnose memory<br>pressure|
|uptme|System|Beginner|Load average, uptme|-|Quick health check|



Page 117 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Command**|**Category**|**Difculty**|**What It Does**|**Key**<br>**Opton**|**DevOps Use Case**|
|---|---|---|---|---|---|
|uname|System|Beginner|Kernel/system info|-a|Identfy OS/kernel|
|dmesg|System|Intermedi<br>ate|Kernel ring bufer|-T|Find OOM kills, hardware<br>errors|
|vmstat /<br>iostat / sar|Performance|Advanced|Resource stats over tme|-x, 2|Diagnose I/O/CPU<br>botlenecks|
|mkfs / fdisk /<br>lsblk|Storage|Advanced|Partton/format disks|-l, -f|Prepare new disk volumes|
|mount /<br>umount|Storage|Intermedi<br>ate|Atach/detach flesystems|-t, -o|Atach volumes|
|dd|Storage|Advanced|Raw block copy|if=, of=|Disk cloning (high risk)|
|gzip / zip|Archiving|Beginner|Compress fles|-r|Compress logs/artfacts|
|visudo|Privilege|Advanced|Safely edit sudoers|-|Grant sudo access safely|
|ssh-keygen|SSH|Intermedi<br>ate|Generate SSH keys|-t<br>ed25519|Set up key-based auth|
|ssh-copy-id|SSH|Beginner|Install a public key remotely|-i|Enable passwordless SSH|
|git<br>clone/add/com<br>mit/push|Git|Beginner|Core version control|-|Every code change|
|git<br>branch/switch/<br>merge|Git|Intermedi<br>ate|Branch workfow|-c, --no-f|Feature development|
|git rebase|Git|Advanced|Replay commits linearly|-i|Clean history before PR|
|git refog|Git|Advanced|Recover lost commits|-|Undo destructve mistakes|
|git bisect|Git|Advanced|Binary-search for a bad<br>commit|-|Root-cause a regression|
|docker build|Docker|Beginner|Build an image|-t|CI/CD build stage|
|docker run|Docker|Beginner|Start a container|-d, -p, -e|Run an applicaton|
|docker ps /<br>logs|Docker|Beginner|Inspect containers|-a, -f|Troubleshoot containers|
|docker exec|Docker|Beginner|Shell into a container|-it|Interactve debugging|
|docker system<br>prune|Docker|Intermedi<br>ate|Reclaim disk space|-a --<br>volumes|Clean up build agents|
|docker<br>compose<br>up/down|Docker|Beginner|Mult-container apps|-d|Local dev environments|
|kubectl get|Kubernetes|Beginner|List resources|-o wide, -<br>A|Cluster state overview|



Page 118 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Command**|**Category**|**Difculty**|**What It Does**|**Key**<br>**Opton**|**DevOps Use Case**|
|---|---|---|---|---|---|
|kubectl<br>describe|Kubernetes|Beginner|Resource details + events|-|Diagnose pod issues|
|kubectl logs|Kubernetes|Beginner|Container logs|-f, --<br>previous|App-level debugging|
|kubectl exec|Kubernetes|Beginner|Shell into a pod|-it|Interactve debugging|
|kubectl apply|Kubernetes|Beginner|Declaratve deploy|-f|Deploy manifests|
|kubectl rollout|Kubernetes|Intermedi<br>ate|Manage deploy lifecycle|status,<br>undo|Watch/rollback releases|
|kubectl scale|Kubernetes|Beginner|Change replica count|--replicas|Manual scaling|
|kubectl port-<br>forward|Kubernetes|Intermedi<br>ate|Local access to a pod/svc|-|Debug internal services|
|kubectl confg|Kubernetes|Intermedi<br>ate|Manage contexts|use-<br>context|Switch clusters safely|
|kubectl top|Kubernetes|Intermedi<br>ate|Live resource usage|-|Spot resource pressure|
|terraform<br>init/plan/apply|IaC|Beginner|Core Terraform workfow|-out|Provision infrastructure|
|terraform<br>destroy|IaC|Advanced|Tear down infrastructure|-|Remove temp<br>environments|
|terraform state|IaC|Advanced|Inspect/manage state|list, show|Manage resource tracking|
|ansible-<br>playbook|Automaton|Intermedi<br>ate|Run a playbook|--check, --<br>dif|Confguraton<br>management|
|ansible-vault|Automaton|Intermedi<br>ate|Encrypt secrets|view, edit|Store secrets safely|
|aws / az /<br>gcloud|Cloud|Intermedi<br>ate|Cloud provider CLIs|confgure,<br>auth|Manage cloud resources|
|aws sts get-<br>caller-identty|Cloud|Beginner|Verify current identty|-|Confrm account/role<br>before actng|
|aws s3|Cloud|Beginner|Object storage operatons|cp, sync|Artfact/backup storage|
|apt / dnf|Packages|Beginner|Package management|install,<br>update|Install sofware, patch<br>systems|
|env / export|Shell|Beginner|Environment variables|-|App/CI confguraton|
|tee|Shell|Intermedi<br>ate|Duplicate output to<br>fle+stdout|-a|Log while watching live|
|logrotate|Logs|Intermedi<br>ate|Rotate/compress logs|-f, -d|Prevent disk-full from logs|
|nsenter|Advanced|Advanced|Enter another process's<br>namespaces|-t, -n|Debug container<br>networking from host|



Page 119 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

|**Command**|**Category**|**Difculty**|**What It Does**|**Key**<br>**Opton**|**DevOps Use Case**|
|---|---|---|---|---|---|
|sysctl|Advanced|Advanced|Kernel runtme parameters|-w|Tune network/kernel<br>behavior|
|ulimit|Advanced|Intermedi<br>ate|Per-process resource limits|-n|Fix 'too many open fles'|
|perf|Advanced|Advanced|CPU profling|top,<br>record|Functon-level<br>performance analysis|
|stat|Files|Beginner|File metadata|-|Check modifcaton tmes|
|column|Text|Beginner|Format columns|-t|Readable CSV/delimited<br>output|
|hostnamectl /<br>tmedatectl|System|Beginner|Hostname/tme confg|set-<br>hostname|Server identty and clock<br>sync|
|lscpu / lsblk|System|Beginner|Hardware inventory|-|Understand instance specs|



Page 120 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **36. DevOps Command Cheat Sheet** 

A condensed, category-organized quick reference. Keep this chapter bookmarked for daily work. 

#### **Files** 

```
ls -la
cp -a src dst
mv src dst
rm -rf path
find . -name '*.log' -mtime +7
tar -czvf out.tar.gz dir/
```

#### **Permissions** 

```
chmod 755 file
chmod +x script.sh
chown user:group file
umask 022
```

#### **Processes** 

```
ps aux --sort=-%cpu | head
top
kill -15 PID
kill -9 PID
pkill -f name
nohup cmd &
```

#### **Networking** 

```
ip addr
ip route
ping -c 4 host
ss -tulpn
nc -zv host port
traceroute host
mtr host
```

#### **DNS** 

```
dig example.com
dig -x IP
nslookup example.com
cat /etc/resolv.conf
resolvectl status
```

#### **SSH** 

```
ssh -i key user@host
```

Page 121 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
scp -r dir user@host:/path
rsync -avz src user@host:/path
ssh-keygen -t ed25519
ssh -L 8080:remote:80 user@host
```

#### **Logs** 

```
journalctl -u svc -f
journalctl --since '1 hour ago'
tail -f /var/log/app.log
grep -i error app.log
zgrep error app.log.1.gz
```

#### **Storage** 

```
df -h
df -i
du -sh /var/* | sort -rh
lsblk
mount | grep path
```

#### **Services** 

```
systemctl status svc
systemctl restart svc
systemctl enable svc
systemctl --failed
```

#### **Git** 

```
git status
git add -A && git commit -m 'msg'
git push origin branch
git log --oneline --graph
git rebase main
git reflog
```

#### **Docker** 

```
docker build -t app:tag .
docker run -d -p 8080:80 app:tag
docker ps -a
docker logs -f container
docker exec -it container sh
docker system prune -af
```

#### **Kubernetes** 

```
kubectl get pods -o wide
kubectl describe pod name
```

Page 122 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

```
kubectl logs pod -f
kubectl apply -f file.yaml
kubectl rollout status deployment/name
kubectl rollout undo deployment/name
```

#### **AWS** 

```
aws sts get-caller-identity
aws s3 sync ./dist s3://bucket/
aws ec2 describe-instances
aws eks update-kubeconfig --name cluster
```

#### **Terraform** 

```
terraform init
terraform plan -out=tfplan
terraform apply tfplan
terraform state list
terraform output
```

#### **Ansible** 

```
ansible all -m ping
ansible-playbook site.yml --check --diff
ansible-vault view secrets.yml
```

#### **Troubleshooting** 

```
top / htop
df -h && df -i
ss -lntp
journalctl -p err -b
kubectl describe pod name
docker logs -f container
```

Page 123 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **37. Linux & Networking Commands — DevOps Interview Questions** 

50+ practical questions organized by topic, with concise answers you can use to check or refresh your own understanding. 

#### **37.1 Linux Fundamentals** 

###### **Q: How do you find the largest files on a server?** 

A: `du -sh /var/* | sort -rh | head` for directories, or `find / -xdev -type f -size +100M -exec ls -lh {} \;` for individual large files. 

###### **Q: Difference between `df` and `du`?** 

A: `df` reports filesystem-level space from the kernel's block accounting; `du` sums file sizes by walking the visible directory tree. They can disagree when a file is deleted but still held open by a running process — df still counts that space, du can't see it. 

###### **Q: Difference between `kill` and `kill -9`?** 

A: Plain `kill` sends SIGTERM (15), a graceful shutdown request the process can catch and clean up after. `kill -9` sends SIGKILL, an immediate, uncatchable termination at the kernel level — no cleanup, use only when SIGTERM fails. 

###### **Q: How do you check which process is using a port?** 

A: `sudo ss -tulpn | grep :PORT` or `sudo lsof -i :PORT`. 

###### **Q: How do you find a process consuming the most memory?** 

A: `ps aux --sort=-%mem | head` or sort by memory (`M`) inside `top`/`htop`. 

###### **Q: What's the difference between a hard link and a symbolic link?** 

A: A hard link is another directory entry pointing to the same inode (same data, same filesystem, survives the original being deleted). A symlink is a separate file containing a path reference — it can cross filesystems but breaks if the target is removed. 

###### **Q: What are zombie and orphan processes?** 

A: A zombie is a finished process still listed in the process table because its parent hasn't collected its exit status. An orphan is a process whose parent exited before it did; it gets re-parented to init/systemd (PID 1), which will reap it. 

###### **Q: How do you find files modified in the last 24 hours?** 

A: `find /path -mtime -1` (or `-mmin -1440` for minute-level precision). 

###### **Q: What does `chmod 755` mean?** 

A: Owner: read/write/execute (7); group: read/execute (5); others: read/execute (5) — typical for executable scripts/binaries. 

###### **Q: What is inode exhaustion and how do you diagnose it?** 

A: A filesystem running out of inodes (metadata slots) even though disk space remains, usually from huge numbers of small files. Diagnose with `df -i`; a high IUse% alongside free disk space is the signature. 

#### **37.2 Processes & Performance** 

###### **Q: How do you troubleshoot high CPU usage on a production server?** 

A: Start with `top`/`htop` to find the offending process, `ps -p PID -o ... etime` for context, check per-thread usage with `top -H -p PID`, review recent logs and deploys around the spike's start time, capture a profile/stack trace if possible, then restart if needed to restore availability before deeper root-causing. 

###### **Q: How do you troubleshoot high memory usage / potential OOM kills?** 

Page 124 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

A: `free -h` for overall pressure, `ps aux --sort=-%mem` to find the top consumer, `dmesg -T | grep -i 'out of memory'` to confirm the OOM killer acted, then profile/fix the app or increase memory limits. 

###### **Q: What's the difference between load average and CPU utilization?** 

A: CPU utilization is the percentage of CPU time in use right now. Load average is the average number of processes runnable or waiting (including for I/O) over 1/5/15 minutes — it can be high even when CPU% looks moderate if processes are blocked on I/O. 

###### **Q: How would you find out what a hung process is stuck doing?** 

A: `strace -p PID` to see its current/blocking syscall, or `lsof -p PID` to see what files/sockets it holds. 

###### **Q: What causes 'too many open files' errors and how do you fix them?** 

A: The process has hit its file descriptor limit (`ulimit -n`). Check current usage with `lsof -p PID | wc -l`, raise the limit in the process's systemd unit or `/etc/security/limits.conf`, and investigate whether the app is leaking file descriptors. 

#### **37.3 Networking** 

###### **Q: How do you check listening ports on a server?** 

A: `ss -tulpn` (modern) or `netstat -tulpn` (legacy). 

###### **Q: How do you troubleshoot DNS resolution failures?** 

A: Check `/etc/resolv.conf` and `resolvectl status` for configured resolvers, run `dig <domain>` against the default resolver, then `dig @8.8.8.8 <domain>` against a known-good public resolver to isolate local vs. authoritative-side problems. 

###### **Q: What's the difference between TCP and UDP?** 

A: TCP is connection-oriented with guaranteed, ordered delivery and retransmission (HTTP, SSH, databases). UDP is connectionless with no delivery guarantee but lower overhead (DNS queries, streaming, some metrics protocols). 

###### **Q: How do you test if a remote port is reachable?** 

A: `nc -zv host port` or `telnet host port`; for HTTP(S) specifically, `curl -v host:port`. 

###### **Q: Explain the difference between `ping` and `traceroute`.** 

A: `ping` tests basic end-to-end reachability and round-trip time. `traceroute` reveals every intermediate hop along the path, useful for pinpointing where latency or a break occurs. 

###### **Q: What HTTP status code indicates a load balancer can't reach any backend?** 

A: 502 Bad Gateway (or 503 Service Unavailable, depending on the LB/proxy and whether it's an upstream connection failure vs. no capacity). 

###### **Q: How do you capture and inspect live network traffic?** 

A: `tcpdump`, scoped tightly with host/port filters and `-c` to limit packet count, optionally writing to a `.pcap` file with `-w` for offline analysis (e.g., in Wireshark). 

###### **Q: What's the difference between a local and remote SSH port forward?** 

A: Local forwarding (`-L`) exposes a remote service on your local machine. Remote forwarding (`-R`) exposes a local service to the remote host/network — the tunnel direction is reversed. 

###### **Q: Why might `ping` fail while the actual service is up?** 

A: Many networks/firewalls block ICMP for security while still allowing TCP traffic on application ports — always confirm with `curl`/`nc` at the transport/application layer as well. 

###### **Q: How do you find which process is generating unexpected outbound traffic?** 

A: Combine `ss -tp` (or `lsof -i`) to map active connections to PIDs, then `tcpdump` scoped to the suspicious destination for packet-level detail. 

Page 125 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **37.4 Services, Logs & Storage** 

###### **Q: How do you troubleshoot a failed systemd service?** 

A: `systemctl status <service>` for the immediate error and exit code, then `journalctl -u <service> -n 100` for detailed logs, verify config syntax if the app supports a test flag, check dependent resources (disk, ports, permissions), then restart and re-verify. 

###### **Q: How do you find errors in logs efficiently?** 

A: `grep -i error /path/to/log`, or for systemd services `journalctl -u service -p err`; for compressed rotated logs use `zgrep` instead of manually decompressing. 

###### **Q: What's the difference between `systemctl restart` and `systemctl reload`?** 

A: `restart` fully stops and starts the process (drops connections/state). `reload` asks the running process to re-read its configuration without a full restart, if the application supports it — preserving active connections. 

###### **Q: Why would `df` show a filesystem full while `du` doesn't account for all the space?** 

A: A file was deleted while still held open by a running process; the space isn't released until the process closes the file handle or is restarted. Find such files with `lsof | grep deleted`. 

###### **Q: What is logrotate and why does it matter in production?** 

A: A utility that rotates, compresses, and eventually deletes log files on a schedule, preventing unbounded log growth from filling the disk — a standard, essential part of any production server. 

###### **Q: How do you safely edit a production config file?** 

A: Back it up first (`cp file file.bak`), make the edit, validate syntax if the application supports a test/check flag (e.g. `nginx -t`), then reload/restart and verify. 

#### **37.5 Docker & Kubernetes** 

###### **Q: How do you troubleshoot a Kubernetes pod in CrashLoopBackOff?** 

A: `kubectl describe pod` for events (OOMKilled, failing probes), `kubectl logs pod --previous` to see the crashed container's own output (the current instance may not have logged anything useful yet), then fix the underlying app/config/resource issue and confirm a stable restart count. 

###### **Q: How do you troubleshoot ImagePullBackOff?** 

A: `kubectl describe pod` to see the exact pull error — wrong image/tag, missing registry credentials (imagePullSecrets), or network/DNS issues from the node to the registry. 

###### **Q: How do you check if a Kubernetes Service is routing to healthy pods?** 

A: `kubectl get endpoints <service>` — an empty list means the Service's label selector matches no Ready pod. 

###### **Q: How do you roll back a bad Kubernetes deployment?** 

A: `kubectl rollout undo deployment/<name>` (optionally `--to-revision=N` for a specific prior version), then `kubectl rollout status` to confirm it completes. 

###### **Q: Why might a Docker container work locally with `docker run` but fail in Kubernetes?** 

A: Common causes: differing environment variables/ConfigMaps, resource limits triggering OOM kills, missing Secrets, or the container relying on host-only bind mounts/network access not present in the cluster. 

###### **Q: How do you free up disk space on a Docker host?** 

A: `docker system df` to see usage by category, then `docker system prune -a` (add `--volumes` cautiously) to remove unused images/containers/networks/volumes. 

###### **Q: What does OOMKilled: true mean in `docker inspect` / pod status?** 

A: The container exceeded its memory limit and the kernel's OOM killer terminated it — fix by increasing the memory limit (if justified) or resolving a memory leak. 

Page 126 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

#### **37.6 Git, CI/CD & IaC** 

###### **Q: How do you recover a commit after an accidental `git reset --hard`?** 

A: `git reflog` to find the prior HEAD position, then `git reset --hard <ref>` to restore it — reflog retains history even after operations that appear to discard it. 

###### **Q: What's the difference between `git merge` and `git rebase`?** 

A: `merge` preserves both histories and creates a merge commit; `rebase` replays commits onto a new base, producing linear history but rewriting commit hashes — never rebase commits already shared/pushed unless the team agrees. 

###### **Q: Why should `terraform plan` always precede `terraform apply` in production?** 

A: `plan` shows exactly what will be created, changed, or destroyed without making any changes — it's the review gate that catches unintended destructive changes (e.g. from a variable typo) before they happen. 

###### **Q: What is Terraform state and why is it important?** 

A: A file tracking the mapping between your configuration and real-world resource IDs; Terraform uses it to compute diffs on every plan/apply. Losing or corrupting it can make Terraform lose track of existing infrastructure. 

###### **Q: What does 'idempotent' mean in the context of Ansible?** 

A: Running the same playbook multiple times produces the same end state without unintended side effects or duplicate changes — a core design principle of configuration management tools. 

###### **Q: How would you debug a CI/CD pipeline failing only at the deploy stage?** 

A: If build/test passed, suspect environment-specific issues: expired/missing credentials, target-environment connectivity, or drift between the CI runner and the deploy target rather than the code change itself. 

#### **37.7 General & Scenario-Based** 

###### **Q: How do you troubleshoot an unreachable server end to end?** 

A: Work outward: local network config → DNS → routing → firewall/security group → load balancer → server → application — confirming each layer before moving to the next, rather than guessing. 

###### **Q: A teammate ran `rm -rf` on the wrong directory in production. What do you check first?** 

A: Whether the data is recoverable from backups/snapshots, whether any process still holds deleted files open (which could allow limited recovery via `/proc/<pid>/fd/`), and immediately assess blast radius before deciding next steps. 

###### **Q: How do you verify a TLS certificate is valid and not expiring soon?** 

A: `openssl s_client -connect host:443 -servername host` or `curl -vI https://host` and inspect the certificate dates in the output. 

###### **Q: What's your first command when SSH access to a server suddenly stops working?** 

A: `ssh -v` for verbose connection diagnostics locally, and if that's inconclusive, check reachability at the network layer (`nc -zv host 22`) before assuming it's an SSH/auth-specific issue versus the host being down entirely. 

###### **Q: How do you confirm which cloud account/subscription/project your current CLI session is targeting before a destructive action?** 

A: `aws sts get-caller-identity`, `az account show`, or `gcloud config list` — always confirm identity/context before running anything with `delete`, `destroy`, or `terminate` semantics. 

Page 127 of 128 

_Reference Edition_ 

DevOps Linux & Networking Handbook 

### **38. DevOps Learning Roadmap** 

#### **Level 1 — Beginner: Linux Fundamentals** 

Focus on comfort with the shell: navigation, file management, permissions, viewing/searching text. Commands: pwd, ls, cd, cp, mv, rm, cat, less, head, tail, grep, chmod, chown, find. 

#### **Level 2 — Intermediate: Processes, Services, Networking, Storage, Bash, SSH, Git** 

Understand how a running system works end to end: process management (ps, top, kill), systemd (systemctl, journalctl), storage (df, du, mount), core networking (ip, ping, curl, ss, dig), shell scripting fundamentals (variables, pipes, redirection), SSH-based remote access, and everyday Git. 

#### **Level 3 — Advanced: Networking Troubleshooting, Performance, Security, Automation** 

Deepen into packet-level networking (tcpdump), performance analysis (vmstat, iostat, sar, strace, perf), firewall management (iptables/nftables), and basic automation (cron, systemd timers, shell scripting for real tasks). 

#### **Level 4 — DevOps: Docker, Kubernetes, CI/CD, Cloud CLI, Terraform, Ansible** 

Move into containerization and orchestration (Docker, Docker Compose, kubectl), Infrastructure as Code (Terraform), configuration management (Ansible), cloud provider CLIs (AWS/Azure/GCP), and CI/CD pipeline design. 

#### **Level 5 — Production / SRE: Troubleshooting, Observability, Incident Response** 

Combine everything into fast, methodical incident response: reading the right signal quickly, following a troubleshooting chain instead of guessing, understanding reliability trade-offs (rollback vs. fix-forward), and building the muscle memory this handbook's playbooks are designed to train. 

**Note:** Revisit the troubleshooting playbooks in Chapter 32 periodically — real fluency comes from practicing the diagnostic sequence until it's automatic, not from memorizing command syntax alone. 

Page 128 of 128 


