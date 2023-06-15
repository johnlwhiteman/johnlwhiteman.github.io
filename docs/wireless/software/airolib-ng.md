# Airolib-ng

## Commands

* Run [setup](../setup.md) first

```bash
# Create list of one or more SSIDs
echo $SSID > $SSID.txt

# Import that list into a new airolib-ng database
airolib-ng $SSID.sqlite --import essid $SSID.txt

# Query the imported list
airolib-ng $SSID.sqlite --stats

# Import John's password WORDLIST
airolib-ng $SSID.sqlite --import passwd $WORDLIST

# Batch process the WORDLIST for each SSID
airolib-ng wifu.sqlite --batch

# Query the results
airolib-ng wifu.sqlite --stats

# Krakatoa the password
aircrack-ng -r $SSID.sqlite $PCAP
```

## References

* [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)
* [Airolib-ng](https://www.aircrack-ng.org/doku.php?id=airolib-ng)
