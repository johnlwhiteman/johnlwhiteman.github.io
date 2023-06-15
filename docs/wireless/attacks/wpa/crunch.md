# Crunch with Aircrack-ng (WPA/WPA2)

Use this tool to crack WPA/WPA2 passwords with aircrack-ng

## Commands

```bash
# Pipe crunch's generated passwords to aircrack-ng
crunch 11 11 -t password%%% | aircrack-ng -e $SSID $PCAP -w -
```

```bash
# Some other ways to generate passwords
crunch 8 9
crunch 8 9 abc123

# @ represents lowercase characters or characters from a defined set
# , represents uppercase characters
# % represent numbers
#^ represents symbols

crunch 11 11 -t password%%%
crunch 11 11 0123456789 -t password@@@
crunch 1 1 -p abcde12345
crunch 1 1 -p dog cat bird
crunch 5 5 -t ddd%% -p dog cat bird
```

## Reference

* [Crunch - Wordlist Generator](https://sourceforge.net/projects/crunch-wordlist/)
