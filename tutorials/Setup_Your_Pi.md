# Setup Your Pi

This is a tutorial to setup your *Raspberry Pi Model B 512MB* for audio processing.

## Getting Started

We're going to use [CCRMA's Sattelite build](https://ccrma.stanford.edu/~eberdahl/Satellite/) to make configuration on the Pi easy.

## Step 1
Download the the latest MicroSDHC card image from the site. This is a large file, approx. 2.8 gigs.

## Step 2
Visit [CCRMA's setup tutorial page](https://ccrma.stanford.edu/wiki/How_To_Get_Satellite_CCRMA) for more details.

In a nutshell, uncompress the disk image.

Run the command 
```sh
$ df
```

unmount the diskimage (find the correct image. it may be /dev/disk1s1 for example) 
```sh
$ diskutil unmountDisk /dev/disk2s1
```

cd to the correct folder. Then run the following to the same disk number 
```sh
$ sudo dd if=SatelliteCCRMA_Rpi_v0.99.5.dd of=/dev/disk2 bs=1m
```

Note: this will take some time...

To check the status on OSX, inside a new terminal window use 
```sh
$ sudo killall -INFO dd
```

The final message should read 
```sh
7822376960 bytes transferred in 2086.223201 secs (3749540 bytes/sec)
```

Now you can load the SD card into your Raspberry Pi. On first initialization, remove all USB connections (keyboard, mouse, wifi, etc).

## Required Hardware for Raspberry Pi

* Raspberry Pi 512MB Model B
* 8GB SDHC card (Find the appropriate Satellite
* CCRMA SDHC card image on the main page.)
* Retractable USB cable (e.g. from GT Max)
* Ethernet cable
* Either a USB micro cable to power the Raspberry Pi from your laptop or a high-quality micro USB power supply (Note: Do not use cell phone battery chargers to power the Raspberry Pi. This will adversely affect the audio quality.)
* Arduino Nano
* Solderless breadboard