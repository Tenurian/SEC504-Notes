# CTF Cheat Sheet <!-- omit in toc -->

- [Linux CLI](#linux-cli)
  - [A](#a)
    - [awk](#awk)
  - [c](#c)
    - [curl](#curl)
  - [G](#g)
    - [grep](#grep)
  - [H](#h)
    - [hashcat](#hashcat)
    - [head](#head)
  - [J](#j)
    - [john](#john)
    - [jq](#jq)
  - [L](#l)
    - [less](#less)
  - [M](#m)
    - [man](#man)
    - [masscan](#masscan)
    - [md5sum](#md5sum)
  - [N](#n)
    - [nano](#nano)
    - [nmap](#nmap)
  - [S](#s)
    - [sed](#sed)
    - [script](#script)
  - [T](#t)
    - [tail](#tail)
    - [tcpdump](#tcpdump)
  - [W](#w)
    - [w](#w-1)
    - [who](#who)
  - [Z](#z)
    - [zgrep](#zgrep)
- [Metasploit](#metasploit)
  - [Automation](#automation)
  - [msfconsole](#msfconsole)
    - [Arguments](#arguments)
    - [Commands](#commands)
  - [meterpreter](#meterpreter)
    - [msfvenom](#msfvenom)
- [Windows CLI](#windows-cli)
  - [C](#c-1)
    - [certutil](#certutil)
  - [S](#s-1)
    - [schtasks](#schtasks)
    - [strings](#strings)
- [Volatility Framework](#volatility-framework)
- [OS Agnostic CLI](#os-agnostic-cli)
  - [N](#n-1)
    - [netcat, ncat, nc](#netcat-ncat-nc)
  - [W](#w-2)
    - [whoami](#whoami)
- [Linux GUI Applications](#linux-gui-applications)
  - [BeEF](#beef)
- [Windows GUI Applications](#windows-gui-applications)
  - [R](#r)
    - [RegEdit](#regedit)
  - [S](#s-2)
    - [Services.msc](#servicesmsc)
    - [Sysinternals](#sysinternals)
  - [T](#t-1)
    - [Task Scheduler](#task-scheduler)
- [OS Agnostic GUI Applications](#os-agnostic-gui-applications)
  - [S](#s-3)
    - [Spiderfoot](#spiderfoot)
- [Cloud Tools](#cloud-tools)


# Linux CLI

## A
### awk
- `-F` define the Field Separator
  - `awk -F:` will split whatever you give it on the `:` character

## c
### curl
`curl http://some_website_or_ip` downloads the files located on some website or ip

## G
### grep
`grep "some string" /path/to/file` looks for some string in file
- `-e` allows for the use of regex
- `-i` case insensitive mode
- `-v` returns the contents of the file _without_ the matching lines

## H
### hashcat
`hashcat some_file_of_hashes` attempts to crack the hashes
- `-a`
- `-m`

### head
`head somefile` prints the top lines of the file
- `-1` through `-20` will print the top _n_ lines of the file, based on what number follows the -

## J
### john
`john some_file_of_credentials` attempts to crack passwords
- `--format=FORMAT` tells john what format the credentials are
- `--wordlist=/path/to/wordlist.txt` tells john which wordlist to use

### jq
`jq {some_regex_pattern} some_json_file.json` parses the json file and returns key/value pairs that match `some_regex_pattern`

## L
### less
`less somefile` prints an amount of lines in the file

## M
### man
`man some_command` shows the manual pages for some_command, if they exist

### masscan
`sudo masscan {NETWORK_ID/CIDR}` scans a large range of IPs very quickly
- `-p` define the ports to scan

### md5sum
`md5sum some_file` calculates the MD5 sum of some_file

## N
### nano

### nmap
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

## S
### sed
`sed "s/somepattern/replacement/" file_or_string` replaces instances of somepattern with replacement 

### script
enables logging of the current shell

## T
### tail
`tail somefile` prints the bottom lines of the file
- `-1` through `-20` will print the bottom _n_ lines of the file, based on what number follows the -

### tcpdump
- `-n` disables name resolution

## W
### w
`w` prints a list of all currently logged on users and what they're doing
### who
`who` prints a list of all currently logged on users

## Z
### zgrep
`zgrep 'somestring' some_compressed_file.gz` looks through a compressed file or archive to find specific text

# Metasploit

## Automation
- Store raw msfconsole commands in `.rc` files and then execute them with
  - `msfconsole -q -r some_rc_file.rc`

## msfconsole
`msfconsole` launches the console
### Arguments
- `-q` launch in quiet mode (slightly faster)

### Commands
- `exploit` / `run`
- `search`
- `use`

## meterpreter
  - `background` puts the current meterpreter session in the background

### msfvenom

# Windows CLI

## C
### certutil
`certutil -hashfile some_file MD5` calculates the MD5 hash of some_file

## S
### schtasks

### strings

# Volatility Framework
`vol.py` runs the volatility framework

# OS Agnostic CLI

## N
### netcat, ncat, nc
`netcat 192.168.0.2 4444` makes a connection to 192.168.0.2 on port 4444
- `-lp {PORT}` opens listener on `{PORT}`
- `-v` turns on verbose mode
- `-u` forces udp traffic

## W
### whoami
`whoami` prints the username of whomever you're currently logged on as

---
---

# Linux GUI Applications

## BeEF

# Windows GUI Applications

## R

### RegEdit

## S

### Services.msc

### Sysinternals
- AutoRuns
- Procdump
- Procexp
- Procmon
- PsExec
- PsList
- Strings
- TCPView

## T

### Task Scheduler

# OS Agnostic GUI Applications

## S
### Spiderfoot

---

# Cloud Tools
