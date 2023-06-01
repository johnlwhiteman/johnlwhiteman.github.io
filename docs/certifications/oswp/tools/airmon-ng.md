# airmon-ng

## Commands

```bash
# Check status and/or listing wireless interfaces
sudo airmon-ng

# Check for processes that might interfere
sudo airmon-ng check

# Check and kill processes that might interfere
sudo airmon-ng check kill

# Start interface in monitor mode
sudo airmon-ng start wlan0

# Start interface in monitor mode and channel is set
sudo airmon-ng start wlan0 3

# Check if interface in monitor mode and channel is set
iw dev wlan0mon info
iwconfig wlan0mon

# Remove the interface in monitor mode
sudo airmon-ng stop wlan0mon
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)


