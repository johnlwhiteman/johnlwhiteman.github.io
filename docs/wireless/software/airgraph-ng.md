# airgraph-ng.md

## Commands

* Run [setup](../setup.md) first

```bash
# Capture some packets
sudo airodump-ng -a --bssid $BSSID -c $CHANNEL -w $TAG $ADAPTER

# Generate a Client to AP Relationship (CAPR) graph
airgraph-ng -o $TAG-capr.png -i $PCAP -g CAPR

# Display it
eog $TAG-capr.png

# Generate a Client Probe Graph (CPG) that displays the relationship between clients and probed networks
airgraph-ng -o $TAG-cpg.png -i $TAG-01.csv -g CPG

# Display it
eog $TAG-cpg.png
```

## References

* [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airgraph-ng](https://www.aircrack-ng.org/doku.php?id=airgraph-ng)