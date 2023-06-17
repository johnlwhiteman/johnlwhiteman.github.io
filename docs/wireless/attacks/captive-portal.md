# Captive Portal

## Commands

* Run [setup](../setup.md) first
* Two terminals are needed
* At least on client associated with the AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $INTERFACE

# Start monitoring to collect data
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap $INTERFACE
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

* [Captive Portal](https://en.wikipedia.org/wiki/Captive_portal)
* [hostapd](https://w1.fi/hostapd/)
* [hostapd-mana](https://github.com/sensepost/hostapd-mana/)
* [hostapd-mana config](https://github.com/sensepost/hostapd-mana/blob/master/hostapd/hostapd.conf)
