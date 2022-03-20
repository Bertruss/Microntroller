# Microntroller

### Small BT controller with client python for use with Rasperry Pi projects.

I have used the HC-05 BT breakout for my implementation, but I can't see why this wouldn't
work with any BT adapter/breakout that uses a serial interface.

## Raspberry Pi configuration

The client uses the pybluez python lib and BT Serial Port Profile, which need to be installed and enabled respectively.

### Enable Serial Port Profile (SPP)

[Source for setting up SPP on Raspberry Pi](https://scribles.net/setting-up-bluetooth-serial-port-profile-on-raspberry-pi/)

The relevant steps from this guide:

(Note: I prefer *vim* for text file editing but the default is *nano*. Substitute your favorite text editor.)

1.  Open the service config file.
```
sudo vim /etc/systemd/system/dbus-org.bluez.service
```

2. Edit the 'ExecStart' line, adding the compatibility flag '-C'
```
ExecStart=/usr/lib/bluetooth/bluetoothd -C
```

3. Add a line below immediately after “ExecStart” line, then save and close the file.
```
ExecStartPost=/usr/bin/sdptool add SPP
```

4. Reload the configuration file.
```
sudo systemctl daemon-reload
```

5. Restart the service.
```
sudo systemctl restart bluetooth.service
```

### Installing Raspberry Pi Bluetooth Utils
These may or may not be pre-installed in the most recent versions of Raspberry Pi OS, but there are some necessary utils for managing BT.
```
sudo apt-get install bluetooth bluez-utils blueman bluez
```


### Pairing with the Raspberry Pi
Pairing the BT module is also necessary, but will require you to configure a unique name for the device, 
or learn it's MAC address.

# TODO: layout these steps
