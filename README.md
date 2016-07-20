# ITSummEL
## Introduction
Story of our works in IoT Academy in [ITRC](http://itrc.ac.ir) at Summer 2016.
## Examples :)
### RPi Configuration
For installing Lamp-RPi on RPi (Automated):

- Donwload Raspbian [here](https://www.raspberrypi.org/downloads/raspbian/)
- Install Raspbian on SDcard with `unzip -p 2016-03-18-raspbian-jessie.zip | sudo dd of=/dev/mmcblk0 bs=32M`

After installation if you want you can grow your partition size:

- Run `sudo fdisk /dev/mmcblk0`
- Check the partition number you wish to delete with the p.
- Use the option d to delete a partition. If there is more than one, **fdisk** will prompt for which one to delete.
- Use the option n to create a new partition. Follow the prompts and ensure you allow enough space for any future resizing that is needed. It is possible to specify a set, human-readable size instead of using sectors if this is preferred.
- Check the partition table to ensure that the partitions are created as required using the p option.
- Write the changes with the w option when you are sure they are correct.
- Run fsck on the partition. `sudo e2fsck /dev/mmcblk0p2`
- Resize partition file system. `sudo resize2fs /dev/mmcblk0p2`

### DHT + Python
For using DHT sensor with your RPi and python you must do the following things:
1. Install GPIO library:

```sh
sudo apt-get install python-dev python-rpi.gpio
```

2. Get dht11.py file and put it next to your project. You can download it form
[here](https://github.com/szazo/DHT11_Python), after downloading zip file of
this project use dht11.py and you remove other files.

3. After all you can write your code :)

```python
import RPi.GPIO as GPIO
import dht11

# initialize GPIO
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)
GPIO.cleanup()

# read data using pin 14
# [you connect data pin of dht sensor to GPIO13 of RPi]
instance = dht11.DHT11(pin = 14)
result = instance.read()

if result.is_valid():
    print("Temperature: %d C" % result.temperature)
    print("Humidity: %d %%" % result.humidity)
else:
    print("Error: %d" % result.error_code)
```
