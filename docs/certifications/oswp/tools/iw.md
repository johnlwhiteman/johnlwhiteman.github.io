# iw

## Commands

```bash
# Get information about a wireless adapater
iw dev
iw dev wlan0 info

iwconfig
iwconfig wlan0

# Get a list of channels/frequencies of a wireless adapter
iw phy phy0 channels

iwlist wlan0 channel

# Set interface in monitor mode
sudo ip link set wlan0mon down # If already running
sudo iw dev wlan0 interface add wlan0mon type monitor
sudo ip link set wlan0mon up
iw dev
sudo tcpdump -i wlan0mon -s 65000  # Inject some traffic

# Connect to protected network
iw wlan0 connect wifu keys 0:abcde d:1:0011223344

iwconfig wlan0 key s:abcde; iwconfig wlan0 essid foo

# Delete VAP interface (Warning: Sometimes everything goes)
sudo iw dev wlan0mon interface del
```


## References