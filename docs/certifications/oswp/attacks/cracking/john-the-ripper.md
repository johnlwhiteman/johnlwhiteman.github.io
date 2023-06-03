# John the Ripper with Aircrack-ng

Use this tool to crack WPA/WPA2 passwords with aircrack-ng

## Commands

```bash
# Pipe john's generated passwords to aircrack-ng
john --wordlist=$WORDLIST --rules --stdout | aircrack-ng -e $SSID $PCAP -w -
```

## Customize Rules

We can create additional test cases by editing existing rules.

```bash
sudo vi /etc/john/john.conf

# Append more numbers to the end of each password
$[0-9]$[0-9]
$[0-9]$[0-9]$[0-9]

# Save and try it out
john --wordlist=/usr/share/john/password.lst --rules --stdout | grep -i password123
```

## References

* [John the Ripper](https://www.openwall.com/john/)