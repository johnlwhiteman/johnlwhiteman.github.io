# airmon-ng

Used to enable monitor mode on wireless interfaces. It may also be used to kill network managers, or go back from monitor mode to managed mode. Entering the airmon-ng command without parameters will show the interfaces status.

## Commands

* Run [setup](../setup.md) first

```bash
# List the available interfaces
sudo airmon-ng

# List programs that could interfere with aircrack tools
sudo airmon-ng check

# Kill the programs that could interfere with aircrack tools
sudo airmon-ng check kill
# To regain later
sudo service NetworkManager start

# Start interface in monitor mode
sudo airmon-ng start $ADAPTER
# OR
ifconfig mon0 down
ifconfig mon0 mode managed
ifconfig mon0 up

# Start interface in monitor mode and channel is set
sudo airmon-ng start $ADAPTER $CHANNEL

# Set interface to a specific channel even if running
sudo iw dev $ADAPTER set channel $CHANNEL

# Verify that channel is set correctly
sudo iw dev $INTERFACE info
iwconfig $INTERFACE

# Stop monitor mode on the given interface
sudo airmon-ng stop $INTERFACE

# Run in debug mode
sudo airmon-ng --debug

# Run in verbose mode
sudo airmon-ng --verbose
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
