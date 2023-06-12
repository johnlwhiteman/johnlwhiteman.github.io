# airdecap-ng

Decrypts WEP/WPA/WPA2 capture files and can be used to filter for a specific BSSID.

## Commands

* Run [setup](../setup.md) first

```bash
# Remove uninteresting frames
sudo airdecap-ng -b $BSSID $PCAP

# Open the newly created file in Wireshark
wireshark $PCAP
```

## References

* [Airodecap-ng](https://www.aircrack-ng.org/doku.php?id=airdecap-ng)