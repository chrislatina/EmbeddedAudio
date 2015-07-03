# Using a USB Audio Interface with Pi

Edit the alsa-base.conf file 
```sh
$ sudo vim.tiny /etc/modprobe.d/alsa-base.conf
```

Change the following option from 
```
options snd-usb-audio index=-2
```
to:
``` 
options snd-usb-audio index=0
```

Now on startup, the USB audio device will load by default.

To manually switch, change the JACK settings. You may need to kill your current jackd server. 
```sh
$ killall jackd
```

use the following to check your audio interfaces 
```sh
$ cat /proc/asound/cards /proc/asound/modules
```

it will export something like the following
```
0 [ALSA           ]: BRCM bcm2835 ALSbcm2835 ALSA - bcm2835 ALSA bcm2835 ALSA
1 [Device         ]: USB-Audio - C-Media USB Audio Device C-Media USB Audio Device at usb-bcm2708_usb-1.2, full speed
0 snd_bcm2835
1 snd_usb_audio
```

Now reboot your pi, your USB-Audio device will then be assigned to hw:0 
```sh
$ sudo reboot
```

Now you can restart supercollider. 
```sh
$ sclang sine.sc
```

From your supercollider workstation on your laptop, send a mesage to start the synth and test the USB audio output
```
s = Server("rpi", NetAddr("192.168.105.106",57110));
s.sendMsg("/s_new", "sine", x = s.nextNodeID, 1, 1, "freq", 400);
Now you should hear sound!
```
Notes:

Set JACKD to use the USB audio interface. The USB interface should be hw:1. Note, that plugging in the audio interface for the first time may reboot the raspberry pi. Since the USB-Audio device I use has a mono input, the -i should be set to 1. In this configuration hw:0 is my USB-Audio device.

Run the following command for PLAYBACK 
```sh
$ jackd -P84 -p32 -t2000 -d alsa -dhw:0 -p 2048 -n 3 -r 48000 -P &
```

Sadly, capture and playback results in dropouts and errors. These appear to be the ideal settings, however the issue with xruns prevails. 
```sh
$ jackd -p32 -t1000 -R -dalsa -dhw:0 -p8192 -n3 -r48000 -D -i 1 -o 2 -s -H &
```

More info on [xruns](http://www.linuxmusicians.com/viewtopic.php?f=27&t=2276) and [linuxaudio](http://wiki.linuxaudio.org/wiki/raspberrypi).

## References
* [supercollider: sc-pd-with-jackd](http://new-supercollider-mailing-lists-forums-use-these.2681727.n2.nabble.com/sc-pd-with-jackd-td5876448.html)
* [linux-audio.com](http://linux-audio.com/jack/)