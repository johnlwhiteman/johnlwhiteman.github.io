# airodump-ng

Used for capturing raw 802.11 frames. It is particularly suitable for collecting WEP IVs and WPA handshakes for the intent of using them with aircrack-ng. If you have a GPS receiver connected to the computer, airodump-ng is capable of logging the coordinates of the found access points.

## Commands

* Run [setup](../setup.md) first

```bash
# Capture all traffic on all channels
sudo airodump-ng $INTERFACE

# Capture traffic filtered by given channel/BSSID
sudo airodump-ng -c 3 --bssid $BSSID $INTERFACE

# Capture traffic filtered by given channel/BSSID and save to PCAP file
sudo airodump-ng -c $CHANNEL --bssid $BSSID --output-format pcap -w $TAG $INTERFACE

# Capture traffic filtered by given channel and ESSID
sudo airodump-ng -c 3 --essid $SSID $INTERFACE

# Scan 2.4/5 GHz simultaneously
sudo airodump-ng --band abg $INTERFACE

# Load capture file in airodump-ng
sudo airodump-ng -r $PCAP

# Load capture file in Wireshark
wireshark $PCAP
```

## References

* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)