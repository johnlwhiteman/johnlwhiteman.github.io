# Reconnaissance

Run these commands before each attack to gather information about the target. Store the information as environment variables in a file called `reconnaissance.txt`. The values below are only used as examples. Change them to reflect the current target.

```bash
# Start monitor mode
sudo airmon-ng start wlan0

# Start monitoring for APs
sudo airodump-ng wlan0mon

# Find target and gather BSSID,CHANNEL,CLIENT,SSID info
# Stop monitoring
qq

# Build an environment file for convenience
vi reconnaissance.txt

export BSSID=9C:53:22:03:18:E1
export CHANNEL=3
export CLIENT=DC:A6:32:E9:B6:BD
export TAG=$SSID
export PCAP=$TAG-01.cap
export RAINBOW=$TAG-rainbow.lst
export SSID=wifu
export WORDLIST=/usr/share/john/password.lst

# Save and source it
source reconnaissance.txt
```