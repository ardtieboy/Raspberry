# Raspberry Pi Blox Neo 6M GPS

First of all, this GPS module is not so easy to use. At least at this moment.
This has something to do with the new Jessie OS. ttyAMA0 --> ttySO
However, there are some usefull links I used

[adafruit](https://learn.adafruit.com/adafruit-ultimate-gps-on-the-raspberry-pi/using-uart-instead-of-usb)

[spellfoundry](http://spellfoundry.com/2016/05/29/configuring-gpio-serial-port-raspbian-jessie-including-pi-3/)

The module is connect to 3,3 V_cc, the GND, RX on pin 8 (TX from the pi) and TX on 10 (RX on the pi).

## Step 1: Enable UART

    sudo nano /boot/config.txt

add the line

    enable_uart=1

## Step 2: Disable the console

    sudo systemctl stop serial-getty@ttyS0.service
    sudo systemctl disable serial-getty@ttyS0.service
    sudo nano /boot/cmdline.txt

remove the line

    console = serial0,115200

reboot

    sudo reboot

## Step 3: Install the client

    sudo apt-get install gpsd gpsd-clients python-gps

## Step 4: Start the client

    sudo killall gpsd
    stty -F /dev/ttyS0 9600
    sudo gpsd /dev/ttyS0 -F /var/run/gpsd.sock

or for visual results:

    cgps -s

### Troubleshooting

    sudo killall gpsd
    sudo gpsd /dev/ttyS0 -F /var/run/gpsd.sock

or check stackexchange for "cant get gps to automatically work after reboot"

### CGPS-config (need to be done once)

    sudo nano /etc/default/gpsd
    Devices="/dev/ttyS0"
    GPSD_OPTIONS="/dev/ttyS0"
    GPSD_SOCKET="/var/run/gpsd.sock"

### Monitor the serial monitor

Settings:

    stty -F /dev/ttyS0

Set baudrate:

    stty -F /dev/ttyS0 9600

Monitor the received input

  cat </dev/ttyS0
