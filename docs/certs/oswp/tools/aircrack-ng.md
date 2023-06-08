# Aircrack-ng

## Commands
```bash

# Crack the key using a wordlist
sudo aircrack-ng -w $WORDLIST -b $BSSID -e $SSID $PCAP

# Crack the key with using a database
aircrack-ng -r $DB $PCAP

# Run benchmark (~15s) to see how many passphrases can be cracked per second
aircrack-ng -S
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [GitHub](https://github.com/aircrack-ng/aircrack-ng)