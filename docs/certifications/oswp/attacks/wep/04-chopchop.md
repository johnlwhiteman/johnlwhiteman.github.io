# Korek ChopChop Attack (Clientless) (WEP)

This attack, when successful, can decrypt a WEP data packet without knowing the key. It can even work against dynamic WEP. This attack does not recover the WEP key itself, but merely reveals the plaintext. However, some access points are not vulnerable to this attack. Some may seem vulnerable at first but actually drop data packets shorter that 60 bytes. If the access point drops packets shorter than 42 bytes, aireplay tries to guess the rest of the missing data, as far as the headers are predictable. If an IP packet is captured, it additionally checks if the checksum of the header is correct after guessing the missing parts of it. This attack requires at least one WEP data packet.

## Commands

* Run [setup](../../setup.md) first



## References

* [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)
* [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)
* [KoreK ChopChop](https://www.aircrack-ng.org/doku.php?id=korek_chopchop)
* [ChopChop Theory](https://www.aircrack-ng.org/doku.php?id=chopchoptheory)
* [REdBlueTeam]()


