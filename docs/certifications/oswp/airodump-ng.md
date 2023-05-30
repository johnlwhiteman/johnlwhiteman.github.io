# airodump-ng

## Commands

```bash
# Capture all traffic on all channels
airodump-ng wlan0mon

# Capture traffic filtered by given channel and BSSID (best)
airodump-ng -c 3 --bssid 9C:53:22:03:18:E1 wlan0mon

# Capture traffic filtered by given channel and ESSID
airodump-ng -c 3 --essid wifu wlan0mon

# Capture traffic and save to PCAP file
sudo airodump-ng -c 3 --bssid 9C:53:22:03:18:E1 --output-format pcap -w wifu-packets wlan0mon

# Read the saved output in Wireshark
wireshark wifu-packets-01.cap
```

## References

* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)