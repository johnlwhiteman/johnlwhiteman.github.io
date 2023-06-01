# Aircrack-ng

## Configuration

```bash
sudo vi /etc/john/john.conf

# Append more numbers to the end of each password
$[0-9]$[0-9]
$[0-9]$[0-9]$[0-9]

# Save and try it out
john --wordlist=/usr/share/john/password.lst --rules --stdout | grep -i password123

```

## Commands

```bash
john --wordlist=\usr\share\john\password.lst --rules --stdout | aircrack-ng -e <ESSID> -w - <capture_file>
```

## References

