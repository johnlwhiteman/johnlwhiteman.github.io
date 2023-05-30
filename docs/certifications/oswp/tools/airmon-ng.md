# airmon-ng

## Commands

```bash
# Get listing/status of connected interfaces
sudo airmon-ng

# Kill other wifi network processes that might interfere (always)
sudo airmon-ng check kill

# Start an interface in monitor mode
sudo airmon-ng start wlan0

# Start an interface in monitor mode with a channel is set
sudo airmon-ng start wlan0 3

# Confirm that an interface in monitor mode
iw dev wlan0mon info

iwconfig wlan0mon

ifconfig wlan0mon

# Remove the interface in monitor mode
sudo airmon-ng stop wlan0mon
```

## References

* [https://www.aircrack-ng.org/doku.php?id=airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)


