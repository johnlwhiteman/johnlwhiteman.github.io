# Aircrack-ng

Aircrack-ng is an 802.11 WEP and WPA/WPA2-PSK key cracking program.


## Commands

* Run [setup](../setup.md) first


### WEP

Aircrack-ng can recover the WEP key once enough encrypted packets have been captured with airodump-ng. This part of the aircrack-ng suite determines the WEP key using two fundamental methods. The first method is via the PTW approach (Pyshkin, Tews, Weinmann). The default cracking method is PTW. This is done in two phases. In the first phase, aircrack-ng only uses ARP packets. If the key is not found, then it uses all the packets in the capture. Please remember that not all packets can be used for the PTW method. This Tutorial: Packets Supported for the PTW Attack page provides details. An important limitation is that the PTW attack currently can only crack 40 and 104 bit WEP keys. The main advantage of the PTW approach is that very few data packets are required to crack the WEP key.

```bash


```

### WPA/WPA2

For cracking WPA/WPA2 pre-shared keys, only a dictionary method is used. A “four-way handshake” is required as input. For WPA handshakes, a full handshake is composed of four packets. However, aircrack-ng is able to work successfully with just 2 packets. EAPOL packets (2 and 3) or packets (3 and 4) are considered a full handshake.

```bash
# Crack the key using a wordlist
sudo aircrack-ng -w $WORDLIST -b $BSSID -e $SSID $PCAP

# Crack the key with using a database
aircrack-ng -r $DB $PCAP

# Add colorful display
aircrack-ng -0 $PCAP

# Crack a 64-bit WEP key using PTW attack
aircrack-ng -0 -z -n 64 $PCAP

# Run benchmark (~15s) to see how many passphrases can be cracked per second
aircrack-ng -S
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [GitHub](https://github.com/aircrack-ng/aircrack-ng)