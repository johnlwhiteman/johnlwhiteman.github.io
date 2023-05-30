# Aircrack-ng

All of these commands assume that a wireless adapter is connected and that the victim access point is live.

```bash
# Get listing of wireless interfaces
sudo airmon-ng

# Kill other wireless networking applications that might interfere with our work
sudo airmon-ng check kill

# Start interface in monitor mode
sudo airmon-ng start wlan0

# Start interface in monitor mode and set channel
sudo airmon-ng start wlan0 3

# Change the channel with iw (airmon-ng does not support while running)
iw dev wlan0mon set freq 5
iwconfig wlan0mon channel 5

# Remove the interface in monitor mode
sudo airmon-ng stop wlan0mon
```







## References

* [Homepage](https://www.aircrack-ng.org/doku.php?id=Main)
* [GitHub](https://github.com/aircrack-ng/aircrack-ng)