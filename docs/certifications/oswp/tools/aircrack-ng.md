# Aircrack-ng

## Commands
```bash
# Crack the password
sudo aircrack-ng -w $WORDLIST -b $BSSID -e $SSID $PCAP

# Run benchmark (~15s) to see how many passphrases can be cracked per second
aircrack-ng -S
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [GitHub](https://github.com/aircrack-ng/aircrack-ng)