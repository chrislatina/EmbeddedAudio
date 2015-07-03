# Sharing your network with Pi (OSX)

In this tutorial, we will change your static ip from the CCRMA default of **192.168.105.106** to **192.168.2.2** to enable network sharing. You'll need an ethernet cable, an internet connection, some familiarity with vim or nano, and the terminal.

## Ethernet

* connect your Pi to you computer via ethernet cable
* [ssh](https://ccrma.stanford.edu/wiki/CCRMA_Satellite_How_To_Connect_RevC) into your Pi through the terminal (See CCRMA's Satellite tutorial for more details)

![Network Settings](/images/NetworkSettings1.png)

You will be prompted for a password: temppwd

The Satellite configuration sets the static ethernet ip address to 192.168.105.106

## Updating the Ethernet configuration

```sh
$ sudo vim /etc/network/interfaces
```

Use the following settings

```bash
auto eth0
iface eth0 inet static
address 192.168.2.2
netmask 255.255.255.0
gateway 192.168.2.1
```

In OSX, configure your ethernet connection manually to use the IP address: 192.168.2.1. Under Advanced, select DNS and add the public DNS server 8.8.8.8

Lastly open the resolv.conf file by running,

```sh
sudo nano /etc/resolv.conf
```

and add the following nameservers

```bash
nameserver 192.168.2.1
nameserver 8.8.8.8
```

To test your connection, run

```sh
ping google.com
```

Now you should be able to use your laptop's internet connection. Note that if you are on GTWifi, sharing is BLOCKED.

![Network Error](/images/NetworkError.png)

Also, I'd avoid running sudo apt-get update, as this will disturb the delicately curated versions for the packages used on the CCRMA Satellite build.

Note: Getting an RSA key issue? Remove the old key.
```sh
ssh-keygen -R 192.168.2.2
```

## References
* [galem.wordpress.com](https://galem.wordpress.com/2014/10/14/configuring-the-raspberry-pi-to-share-a-macs-internet-connection/)

