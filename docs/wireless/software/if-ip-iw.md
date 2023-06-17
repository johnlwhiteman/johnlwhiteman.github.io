# IF/IP/IW Commands

This page contains a collection of networking commands. Try to avoid using `iwconfig` since it is considered deprecated.

## IF/IP/IW Commands

```bash

# iwlist
sudo iwlist wlan0 frequency

# Info about wireless devices
sudo iw list

# Grab the SSIDs
sudo iw dev wlan0 scan | grep SSID

# Grab channel number
sudo iw dev wlan0 scan | egrep "DS Parameter set|SSID:"

# Put in monitor mode
sudo iw dev wlan0 interface add wlan0mon type monitor

# Set link to up
sudo ip link set wlan0mon up

# Get info
sudo iw dev wlan0mon info

# Capture some frames
sudo tcpdump -i wlan0mon

# Remove (DON'T)
sudo iw dev wlan0mon interface del

# Get regulatory stuff
sudo iw reg get
```




```bash
# Find connect wireless adapters
ifconfig
ip a

# Get information about a wireless adapter
iw dev
iw dev wlan0 info
iwconfig
iwconfig wlan0

# View the channels and frequencies of the wireless adapter
iw phy phy0 channels
iwlist wlan0 channel

# Detect wireless APs
sudo iw dev wlan0 scan | grep SSID
iwlist wlan0 scan | grep SSID

# Get list of the channels the access points are running
sudo iw dev wlan0 scan | egrep "DS\ Parameter\ set|SSID"
iwlist wlan0 scanning | egrep "ESSID|Channel"

# Set AP to monitor mode old school way ... airmon-ng does not work
sudo ip link set wlan0 down
sudo iw wlan0 set monitor control
sudo ip link set wlan0 up

# Connect to an open network by frequency
iw wlan0 connect wifu 2432
iwconfig wlan0 essid wifu freq 2432M

# Connect to a protected network
iw wlan0 connect wifu keys 0:abcde d:1:0011223344
iwconfig wlan0 key s:abcde; iwconfig wlan0 essid wifu

# Set link on
sudo ip link set wlan0mon up
ifconfig wlan0 up

# Set link off
ip link set wlan0 down
ifconfig wlan0 down

# Put interface in monitor mode
sudo iw dev wlan0 interface add wlan0mon type monitor
sudo airmon-ng start wlan0
sudo iwconfig wlan0 monitor

# Verify interface is working by injecting traffic
sudo tcpdump -i wlan0mon -s 65000

# Change the channel of ADAPTER
sudo iw dev wlan0mon set channel 3
sudo iwconfig wlan0mon channel 3

# Put wireless device back to managed mode
sudo iw dev wlan0mon del
sudo iw phy phy0 interface add wlan0 type managed
sudo iwconfig wlan0 mode managed

# Delete VAP interface
# Warning: Sometimes things go wrong, require reboot
sudo iw dev wlan0mon interface del

# Assign an IP address to a wireless interface
sudo ip link set wlan0 down
sudo ip addr add 192.168.123.1/24 dev wlan0
sudo ip link set wlan0 up
```
