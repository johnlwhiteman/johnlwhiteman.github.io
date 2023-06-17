# WPA-Supplicant

## Connect to AP

```bash
sudo wpa_supplicant -i wlan0 -c wifi-client.conf

# sometimes the driver that wpa_supplican uses is specified (different from the driver used for the wifi interface)
sudo wpa_supplicant -Dnl80211 -i wlan0 -c wifi-client.conf

# request an ip by dhcp, once we are connected to an AP
sudo dhclient -v wlan0


# OR MANUALLY
sudo /sbin/ifconfig wlan0 up
sudo /sbin/iwlist wlan0 scan
sudo /sbin/iwconfig wlan0 essid "NetworkName"
sudo /sbin/iwconfig wlan0 key network_key
sudo /sbin/iwconfig wlan0 enc on
sudo dhclient -v wlan0

# OR
sudo iwconfig wlan0 essid <SSID> key s:<KEY>
sudo dhclient -v wlan0

# Open
iwconfig wlan0 essid <SSID>
ifconfig wlan0 up
dhclient -v wlan0

# WEP
iwconfig wlan0 essid <SSID> key <key>
ifconfig wlan0 up
sudo dhclient -v wlan0

# WPA PSK
wpa_passphrase <SSID> <passphrase> >> /etc/wpa_supplicant.conf
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant.conf
sudo dhclient -v wlan0
ping 8.8.8.8

```

## Open Network
```
network={
  ssid="<ESSID>"
  scan_ssid=1
}

# OR

network={
  ssid="<ESSID>"
  scan_ssid=1
  mode=0
  auth_alg=OPEN
  key_mgmt=NONE
}
```

## WEP

```
network={
  ssid="<ESSID>"
  key_mgmt=NONE
  wep_key0="34567"
  wep_tx_keyidx=0
}

network={
  ssid="<ESSID>"
  key_mgmt=NONE
  wep_key0=0304050607
  wep_tx_keyidx=0
}
```
## WPA/2-PSK
```
network={
  ssid="<ESSID>"
  scan_ssid=1
  psk="<passphrase>"
  key_mgmt=WPA-PSK
}

# OR

network={
  ssid="<ESSID>"
  mode=0
  scan_ssid=1
  auth_alg=OPEN
  key_mgmt=WPA-PSK
  proto=WPA
  pairwise=TKIP
  group=TKIP
  psk="<passphrase>"
}
```

## WPA2 Only

```
network={
  ssid="<ESSID>"
  key_mgmt=WPA_PSK
  psk="<passphrase>"
  proto=RSN
  pairwise=CCMP
  group=CCMP
}

# less specific, can work better
network={
  ssid="<ESSID>"
  key_mgmt=WPA_PSK
  psk="<passphrase>"
  proto=RSN
}

# or maybe this is necessary, due to retrocompatibility with old devices
network={
  ssid="<ESSID>"
  key_mgmt=WPA_PSK
  psk="<passphrase>"
  proto=WPA
  pairwise=CCMP
  group=CCMP
}

network={
  ssid="<ESSID>"
  scan_ssid=1
  mode=0
  auth_alg=OPEN
  key_mgmt=WPA_PSK
  psk="<passphrase>"
  proto=RSN
  pairwise=CCMP
  group=CCMP
}
```

## WPA Enterprise

```
network={
  ssid="<ESSID>"
  scan_ssid=1
  key_mgmt=WPA-EAP
  eap=PEAP
  identity="bob"
  password="hello"
  phase1="peaplabel=0"
  phase2="auth=MSCHAPV2"
}

  network={
  ssid="<ESSID>"
  scan_ssid=1
  key_mgmt=WPA-EAP
  eap=PEAP
  identity="bob"
  password="hello"
  phase1="peaplabel=0"
  phase2="auth=GTC"
}

network={
  ssid="<ESSID>"
  scan_ssid=1
  key_mgmt=WPA-EAP
  eap=TTLS
  identity="bob"
  anonymous_identity="anon"
  password="hello"
  phase2="auth=PAP"
}

network={
  ssid="<ESSID>"
  scan_ssid=1
  key_mgmt=WPA-EAP
  eap=TTLS
  identity="bob"
  anonymous_identity="anon"
  password="hello"
  phase2="auth=CHAP"
}

network={
  ssid="<ESSID>"
  scan_ssid=1
  key_mgmt=WPA-EAP
  eap=TTLS
  identity="bob"
  anonymous_identity="anon"
  password="hello"
  phase2="auth=MSCHAPV2"
}
```


## References

* [dh0ck](https://github.com/dh0ck/Wi-Fi-Pentesting-Cheatsheet/blob/main/Wifi/cheatsheet/0%20-%20connect%20to%20networks.md)