# Playbook

* Run [Setup](./setup.md) first

## WEP

### AUTH: OPN

#### Client

* [Deauthentication Attack](./attacks/wep/00-deauth.md) *
* [Fake Authentication Attack](./attacks/wep/01-fakeauth.md)
* [Interactive Attack](./attacks/wep/02-interactive.md)
* [ARP Request Replay Attack](./attacks/wep/03-arpreplay.md)

#### Clientless

* [Deauthentication Attack](./attacks/wep/00-deauth.md)
* [Fake Authentication Attack](./attacks/wep/01-fakeauth.md) *
* [ChopChop Attack](./attacks/wep/04-chopchop.md)
* [Fragmentation Attack](./attacks/wep/05-fragment.md)

### AUTH: SKA

* [Fake Authentication Attack w/PSK](./attacks/wep/01-fakeauthkey.md)

## WPA/2

* [Deauthentication Attack ... then](./attacks/wep/00-deauth.md)
    * [Aircrack-ng](./attacks/wpa/aircrack-ng.md)
    * [Airolib-ng](./attacks/wpa/airolib-ng.md)
    * [Cowpatty](./attacks/wpa/cowpatty.md)
    * [Crunch](./attacks/wpa/crunch.md)
    * [John the Ripper](./attacks/wpa/john-the-ripper.md)
    * [Pyrit](./attacks/wpa/pyrit.md)
    * [Rsmangler](./attacks/wpa/rsmangler.md)

## Misc

### Password Lists
```bash
* /usr/share/wordlists
* /usr/share/john/password.lst ($WORDLIST)
* https://github.com/aircrack-ng/aircrack-ng/blob/master/test/password.lst
```