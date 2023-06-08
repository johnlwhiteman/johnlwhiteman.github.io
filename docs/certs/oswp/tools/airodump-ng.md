# airodump-ng

Used for capturing raw 802.11 frames. It is particularly suitable for collecting WEP IVs and WPA handshakes for the intent of using them with aircrack-ng. If you have a GPS receiver connected to the computer, airodump-ng is capable of logging the coordinates of the found access points.

## Commands

```bash
# Capture all traffic on all channels
airodump-ng wlan0mon

# Capture traffic filtered by given channel/BSSID
airodump-ng -c 3 --bssid $BSSID wlan0mon

# Capture traffic filtered by given channel/BSSID and save to PCAP file
sudo airodump-ng -c $CHANNEL --bssid $BSSID --output-format pcap -w $TAG wlan0mon

# Capture traffic filtered by given channel and ESSID
airodump-ng -c 3 --essid $SSID wlan0mon

# Scan 2.4/5 GHz simultaneously
airodump-ng wlan0 --band abg

# Load capture file in airodump-ng
airodump-ng -r $PCAP

# Load capture file in Wireshark
wireshark $PCAP
```

## References

* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)