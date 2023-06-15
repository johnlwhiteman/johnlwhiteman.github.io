# Setup

## Commands

Run these commands on each system to gather information about the target. Store the information as environment variables in a file called `config` and source it as `source config`. The values below are only used as examples since each system will differ. The name of the variables should be consistent as seen throughout the documentation shown here.

```bash
# Kill stuff that can interfere
sudo airmon-ng check kill

# Find the connected wireless device (3 ways)
ifconfig
ip a

# Determine the ADAPTER name, let's assume wlan0

# Set to monitor mode
sudo airmon-ng start wlan0

# Determine INTERFACE name, let's assume wlan0mon

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng wlan0mon

# Do a quick injection test to ensure it works
sudo aireplay-ng --test wlan0mon

# OR do a better injection test if two interfaces are available
sudo aireplay-ng --test -i wlan1 wlan0mon

# Gather info for config file below: BSSID, SSID, ...

# Stop monitoring
qq

# Build an environment file for convenience
vi config

export SSID=wifu

# MAC address of AP
export BSSID=AA:BB:CC:DD:EE:FF

# AP channel
export CHANNEL=3

# MAC address of client connected to AP
export CLIENT=A1:B2:C3:D4:E5:F6

# Device name of connected Wi-Fi ADAPTER
export ADAPTER=wlan0

# Name of connected Wi-Fi ADAPTER when in monitor mode
export INTERFACE=wlan0mon

# MAC address of connected Wi-FI ADAPTER
export INTERFACEMAC=AB:CD:EF:12:34:56

# Device name of a second connected Wi-Fi ADAPTER (optional)
export ADAPTER2=wlan1

# Name of second connected Wi-Fi ADAPTER when in monitor mode (optional)
export INTERFACE2=wlan1mon

# MAC address of second connected Wi-FI ADAPTER (optional)
export INTERFACEMAC2=56:34:12:EF:CD:AB

# Base name given to PCAP file
export TAG=$SSID

# Name of PCAP file created by airodump.ng
export PCAP=$TAG-01.cap

# Name of rainbow table used for cracking hashes
export RAINBOW=$TAG-rainbow.lst

# Path to default wordlist used for cracking
export WORDLIST=/usr/share/john/password.lst

# Contruct the correct PRGA path name
PRGA=$(echo "$TAG-01-$BSSID.xor" | sed 's/\:/-/'g)

# Save and source it
source config

# Note: it might be easier to copy to ~/.zshrc or ~/.bashrc file instead
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
