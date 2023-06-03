# airdecap-ng

Decrypts WEP/WPA/WPA2 capture files and can be used to strip the wireless headers from an unencrypted wireless capture.

## Commands

```bash
# Remove uninteresting frames
sudo airdecap-ng -b 9C:53:22:03:18:E1 slappy-01.cap

# Open the newly created file in Wireshark
wireshark slappy-01-dec.cap
```

## References

* [Airodecap-ng](https://www.aircrack-ng.org/doku.php?id=airdecap-ng)