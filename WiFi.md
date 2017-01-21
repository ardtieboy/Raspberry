# Raspberry Pi Wifi

## Raspberry Pi 3

Easy peasy. Click right above corner en connect to ssid with correct password

## Raspberry Pi Zero

A bit more difficult since only one USB-port can be active.
First you should update the wpa_supplicant file

    sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

And add below

    network={
        ssid="testing"
        psk="testingPassword"
    }

Where "testing" is replaced by "ScheirBinnen" and "psk" with 7RuUtCcN2s9N. After that, disconnect the keyboard and connect the USB wifi adapter. In the meantime reboot.

    sudo reboot

Normally everything should work
