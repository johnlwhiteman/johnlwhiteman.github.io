# Bettercap

bettercap is a powerful, easily extensible and portable framework written in Go which aims to offer to security researchers, red teamers and reverse engineers an easy to use, all-in-one solution with all the features they might possibly need for performing reconnaissance and attacking WiFi networks, Bluetooth Low Energy devices, wireless HID devices and IPv4/IPv6 networks.

* WiFi networks scanning, deauthentication attack, clientless PMKID association attack and automatic WPA/WPA2 client handshakes capture.
* Bluetooth Low Energy devices scanning, characteristics enumeration, reading and writing.
* 2.4Ghz wireless devices scanning and MouseJacking attacks with over-the-air HID frames injection (with DuckyScript support).
* Passive and active IP network hosts probing and recon.
* ARP, DNS, DHCPv6 and NDP spoofers for MITM attacks on IPv4 and IPv6 based networks.
* Proxies at packet level, TCP level and HTTP/HTTPS application level fully scriptable with easy to implement javascript plugins.
* A powerful network sniffer for credentials harvesting which can also be used as a network protocol fuzzer.
* A very fast port scanner.
* A powerful REST API with support for asynchronous events notification on websocket to orchestrate your attacks easily.
* An easy to use web user interface.
* More!

## Installation

* Install on Kali (usually already installed)

```bash
sudo apt-get install bettercap -y
```

## Commands

* Run [setup](../setup.md) first
* Make sure that the ADAPTER is not already monitoring

```bash
# Set AP to monitor mode old school way ... airmon-ng does not work
sudo ip link set wlan0 down
sudo iw wlan0 set monitor control
sudo ip link set wlan0 up

# Put in interactive mode
sudo bettercap -iface $ADAPTER -silent #-debug

# Set channel
wifi.recon.channel 3

# Run Recon
wifi.recon on

# Show APs
wifi.show

# Clear screen
clear

# Exit
exit
```
* Do same but with ticker at command line

```bash
sudo bettercap -iface $ADAPTER -silent -eval "set ticker.commands 'clear; wifi.show'; wifi.recon on; ticker on"

ticker off
wifi.show

wifi.recon $BSSID
```

## Docker Installation Script

```bash
#!/usr/bin/env bash

installDocker() {
    printf '%s\n' "deb https://download.docker.com/linux/debian bullseye stable" | sudo tee /etc/apt/sources.list.d/docker-ce.list
    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/docker-ce-archive-keyring.gpg
    sudo apt update
    sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
    sudo groupadd docker
    sudo usermod -aG docker $USER
    sudo docker run hello-world
    sudo systemctl stop docker >/dev/null 2>&1
    sudo systemctl stop containerd >/dev/null 2>&1
    sudo systemctl enable docker
    sudo systemctl enable containerd
    sudo systemctl start docker
}

installDockerCompose() {
    sudo apt-get install -y curl
    rm -f /tmp/docker-compose
    url=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep browser_download_url | grep docker-compose-linux-x86_64 | cut -d '"' -f 4 | grep -v "sha")
    curl -L $url -o /tmp/docker-compose
    chmod +x /tmp/docker-compose
    sudo mv /tmp/docker-compose /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
    docker-compose version
}

installDocker
installDockerCompose

# Roobt?
```

## References

* [Bettercap](https://www.bettercap.org/)
* [Bettercap Wi-Fi Module](https://www.bettercap.org/modules/wifi/)