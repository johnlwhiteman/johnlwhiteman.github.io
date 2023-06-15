# Injection Test (WEP/WPA/WPA2)

The injection test determines if your card can successfully inject and determine the ping response times to the Access Point (AP). If you have two wireless cards, it can also determine which specific injection tests can be successfully performed.

* Run [setup](../../setup.md) first
* One terminal needed only
* Use two adapters if available

```bash
# Set interface to monitor mode
sudo airmon-ng start $ADAPTER $CHANNEL

# Do a quick injection test to ensure it works
sudo aireplay-ng --test $INTERFACE

# OR do a better injection test if two interfaces are available
sudo aireplay-ng --test -i $ADAPTER2 $INTERFACE
```

## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [Injection Test](https://www.aircrack-ng.org/doku.php?id=injection_test)

