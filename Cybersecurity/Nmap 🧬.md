# TCP
It is used `-sT`.

---
# SYN

It is used `-sS`.
This has a variety of advantages for us as hackers:

-   It can be used to bypass older Intrusion Detection systems as they are looking out for a full three way handshake. This is often no longer the case with modern IDS solutions; it is for this reason that SYN scans are still frequently referred to as "stealth" scans.
-   SYN scans are often not logged by applications listening on open ports, as standard practice is to log a connection once it's been fully established. Again, this plays into the idea of SYN scans being stealthy.
-   Without having to bother about completing (and disconnecting from) a three-way handshake for every port, SYN scans are significantly faster than a standard TCP Connect scan.

There are, however, a couple of disadvantages to SYN scans, namely:

-   They require sudo permissions in order to work correctly in Linux. This is because SYN scans require the ability to create raw packets (as opposed to the full TCP handshake), which is a privilege only the root user has by default.
-   Unstable services are sometimes brought down by SYN scans, which could prove problematic if a client has provided a production environment for the test.

---
# UDP

Rely on speed over quality (e.g. video sharing).
It is used `-sU`.

When a packet is sent to an open UDP port, there should be no response. When this happens, Nmap refers to the port as being `open|filtered`

UDP scans tend to be incredibly slow in comparison to the various TCP scans (in the region of 20 minutes to scan the first 1000 ports, with a good connection). For this reason it's usually good practice to run an Nmap scan with `--top-ports <number>` enabled. For example, scanning with `nmap -sU --top-ports 20 <target>`. Will scan the top 20 most commonly used UDP ports, resulting in a much more acceptable scan time.

---
# Null, Fin and Xmas

Less used. Only identify ports as being open|filtered, closed or filtered.
- Null scans `-sN` are used when the TCP request is sent with no flags set at all. The target should resppond with a RST (reset flag) if the port is closed.
- Fin scans `-sF`are used when the TCP is sent with FIN flag (used to gracefully close an active connection), Nmap expects a RST (reset flag) if the port is closed.
- Xmas scans `-sX`sends a malformed TCP packet and expects a RST response for closed ports. The flags set are PSH (push), URG (urgent) and FIN (fin).
This scans are ussually used for firewall evasion.

--- May respond with a RST for every port -> **Windows** ---

---
# ICMP

Nmap sends an ICMP packet to each possible IP address for the specified network. If it recieves response, it marks the IP address as being alive.

We use `-sn`. We could scan : 
- `nmap -sn 192.168.1.1-254`
- `nmap -sn 192.168.0.0``

---
# NSE Scripts

The **N**map **S**cripting **E**ngine (NSE) is an incredibly powerful addition to Nmap, extending its functionality quite considerably. NSE Scripts are written in the _Lua_ programming language, and can be used to do a variety of things: from scanning for vulnerabilities, to automating exploits for them. The NSE is particularly useful for reconnaisance, however, it is well worth bearing in mind how extensive the script library is.

There are many categories available. Some useful categories include:

-   `safe`:- Won't affect the target
-   `intrusive`:- Not safe: likely to affect the target  
    
-   `vuln`:- Scan for vulnerabilities
-   `exploit`:- Attempt to exploit a vulnerability
-   `auth`:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
-   `brute`:- Attempt to bruteforce credentials for running services
-   `discovery`:- Attempt to query running services for further information about the network (e.g. query an SNMP server)
Multiple scripts can be run simultaneously by separating them by a comma: `--script=smb-enum-users,smb-enum-shares`.

Some scripts require arguments. These can be given with the `--script-args`. The arguments are separated with commas too.

### Search for scripts
Full list of scripts -> https://nmap.org/nsedoc/
Also they are stores on `/usr/share/nmap/scripts`.

We can use `grep` to find pattern matches.

---
# Firewall Evasion
It uses the option `-Pn`, which tells Nmap to not bother pinging the host before scanning it. This means that Nmap will always terat the target host as being alive, effectively bypassing the ICMP block, but it comes at the price of potencially taking a very long time to complete the scan.
There are other switches that are useful for firewall evasion:
- `-f`: used to fragment the packets making it less likely that the packets will be detected by a firewall or IDS (Intrusion Detection System)
- `-mtu <number>`: it's an alternative to `-f` that provides more control over the size of the packets. Accepts a maximum transmission unit size to use that must be a multiple of 8
- `--scan-delay <time>ms`: used to add a delay between packets sent. Useful if the network is unestable, but also for evading any time-based firewall/IDS triggers which may be in place
- `--badsum`: this is used to generate in invalid chcksum for packets. This switch can be used to determine the presence of a firewall/IDS.

---
