# airgraph-ng.md

## Commands

```bash
# Capture some packets
sudo airodump-ng -a --bssid F0:2F:74:C2:5B:C0 -c 10 -w slams wlan0mon

# Generate a Client to AP Relationship (CAPR) graph
airgraph-ng -o slams-capr.png -i dump-01.csv -g CAPR

# Display it
eog slams-capr.png

# Generate a Client Probe Graph (CPG) that displays the relationship between clients and probed networks
airgraph-ng -o slams-cpg.png -i slams-01.csv -g CPG

# Display it
eog slams-cpg.png
```

## References

* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airgraph-ng](https://www.aircrack-ng.org/doku.php?id=airgraph-ng)