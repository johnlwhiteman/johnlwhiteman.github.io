# Teardown

You want to make sure to clean up things. Don't let the vulnerable AP hang around. Think War Drivers or War Squatters.

```bash
sudo airmon-ng stop $INTERFACE
sudo systemctl start NetworkManager
sudo /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant &
sudo dhclient
```

* Unplug the ADAPTER
* Turn off the vulnerable access point
* Turn off the client if used for testing only
