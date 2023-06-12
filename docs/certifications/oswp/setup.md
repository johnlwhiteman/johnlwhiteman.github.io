# OSWP - Setup

## Commands

Run these commands on each system to gather information about the target. Store the information as environment variables in a file called `config` and source it as `source config`. The values below are only used as examples since each system will differ. The name of the variables should be consistent as seen throughout the documentation shown here.


```bash
# Kill stuff that can interfere
sudo airmon-ng check kill

# Find the connected wireless device (3 ways)
ifconfig
ip a

# Determine DEVICE name, let's assume wlan0

# Set to monitor mode
sudo airmon-ng start wlan0

# Determine interface's monitor mode name, let's assume wlan0mon

# Start monitoring for APs
sudo airodump-ng wlan0mon

# Do a quick injection test to ensure it works
sudo aireplay-ng --test wlan0mon

# OR do a better injection test if two interfaces are available
sudo aireplay-ng --test -i wlan1 wlan0mon

# Gather info for config file below: BSSID, SSID, ...

# Stop monitoring
qq

# Build an environment file for convenience
vi/nano config

export SSID=wifu
export BSSID=AA:BB:CC:DD:EE:FF
export CHANNEL=3
export CLIENT=A1:B2:C3:D4:E5:F6
export DEVICE=wlan0
export INTERFACE=wlan0mon
export INTERFACE2=wlan1mon
export INTERFACEMAC=AB:CD:EF:12:34:56
export TAG=$SSID
export PCAP=$TAG-01.cap
export RAINBOW=$TAG-rainbow.lst
export WORDLIST=/usr/share/john/password.lst

# Save and source it
source config
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [REdBlueTeam](https://youtu.be/_9qJ1Urpn0Y?t=1691)