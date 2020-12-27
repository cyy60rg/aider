## Add udev rules for Android (adb/fastboot)

__Motive__ for adding the rule.  
```
$ adb devices/ fastboot devices
no permissions (missing udev rules? user is in the plugdev group); see [http://developer.android.com/tools/device.html]	Motorola Fastboot Interfac
```

### udev rules file: `/etc/udev/rules.d/51-android.rules`
#### Check 51-android.rules file exists
```
ls /etc/udev/rules.d/51-android.rules
```

Connect the device to usb.  
Then, try cmd : ```$ lsusb```
Output:
```
Bus 001 Device 017: ID 22b8:2e80 Motorola PCS
```
Open the file
```
sudo vim /etc/udev/rules.d/51-android.rules
```

Add the rule with the id values in ``lsusb`` value  
```
# Moto G5Plus(potter) fastboot
SUBSYSTEM=="usb", ATTR{idVendor}=="22b8", ATTR{idProduct}=="2e80", MODE="0666", GROUP="plugdev"
```
Save the file.

Change the file permission
```
sudo chmod a+r /etc/udev/rules.d/51-android.rules
```
Reload the rules
```
sudo udevadm control --reload-rules
```

Disconnect and reconnect the device

