# aireplay-ng

## Commands

```bash
# Check if injection works for given interface
sudo aireplay-ng -9 wlan0mon

# Deauthenticate a client connected to an AP
sudo aireplay-ng -0 1 -a $BSSID -c $CLIENT wlan0mon
```
## References

* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
