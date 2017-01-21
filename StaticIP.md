# Raspberry Pi Static IP

Since connecting through SSH is difficult when there is a dynamic IP, you can choose to make a static ip. This is one by editing the dhcpcd.conf file. (from Raspbian Jessie is 18-03-2016 with Kernal version 4.1.)

    sudo nano /etc/dhcpcd.conf

Next add this:

    interface eth0

    static ip_address=192.168.0.10/24
    static routers=192.168.0.1
    static domain_name_servers=192.168.0.1

    interface wlan0

    static ip_address=192.168.0.200/24
    static routers=192.168.0.1
    static domain_name_servers=192.168.0.1

Where ip_address is the IP address you want for the pi.
Where routers is the IP of the router. Normally this is 192.168.0.1.
Where domain_name_servers is also the same 192.168.0.1.

Next reboot

    sudo reboot

verify

    ifconfig
