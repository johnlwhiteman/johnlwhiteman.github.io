# Rsmangler with Aircrack-ng (WPA/WPA2)

Use this tool to crack WPA/WPA2 passwords with aircrack-ng

```bash
# Create a custom wordlist
echo 'donkey' > wordlist.txt
echo 'burro' >> wordlist.txt
echo 'mule' >> wordlist.txt
echo 'ass' >> wordlist.txt
echo 'dumb' >> wordlist.txt

rsmangler --file wordlist.txt --min 12 --max 13 | aircrack-ng -e $SSID $PCAP -w -
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)
* [Rsmangler](https://digi.ninja/projects/rsmangler.php)
