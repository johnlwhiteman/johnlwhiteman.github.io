# airmon-ng

Used to enable monitor mode on wireless interfaces. It may also be used to kill network managers, or go back from monitor mode to managed mode. Entering the airmon-ng command without parameters will show the interfaces status.

## Commands

```bash
# List the available interfaces
sudo airmon-ng

# List programs that could interfere with aircrack tools
sudo airmon-ng check

# Kill the programs that could interfere with aircrack tools
sudo airmon-ng check kill

# Start interface in monitor mode
sudo airmon-ng start wlan0

# Start interface in monitor mode and channel is set
sudo airmon-ng start wlan0 3

# Set interface to a specific channel even if running
sudo iw dev wlan0 set channel 13

# Verify that channel is set correctly
sudo iw dev wlan0mon info
iwconfig wlan0mon

# Stop monitor mode on the given interface
sudo airmon-ng stop wlan0mon

# Run in debug mode
sudo airmon-ng --debug

# Run in verbose mode
sudo airmon-ng --verbose
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
