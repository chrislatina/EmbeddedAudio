# Running SuperCollider on Pi

The objective of this tutorial is to make sound with your Pi using SuperCollider. I will introduce how to run the Pi headless from your laptop, move a SuperCollider synthedef to the Pi, initialize a SuperCollider server on the Pi, and run it from a networked client, namely your laptop over an ethernet connection. This tutorial assumes you have already [Setup Your Pi](Setup_Your_Pi.md). It also may be useful to read [Sharing your network with Pi (OSX)](Sharing_your_network_with_Pi_(OSX).md).

## Ethernet

If you have completed Sharing your network with Pi (OSX), your IP address will now be *192.168.2.2*!

connect your Pi to you computer via ethernet cable
ssh into your Pi through the terminal

```sh
$ ssh -XY ccrma@192.168.105.106
```

you will be prompted for a password: temppwd

The Satellite configuration sets the static ethernet ip address to *192.168.105.106*.

## SynthDefs

Next we need to move a synthdef from your local machine to the pi

The working directory for SuperCollider exists at ~/Supercollider/synthdefs

Let's create a simple sinewave synthdef called sine.sc

```
(
s.waitForBoot {(
  SynthDef("sine", { arg freq;
        var osc;
        osc = SinOsc.ar(freq, 0, 0.1); // 800 Hz sine
        Out.ar(0, osc); // send output to audio bus zero.
    }).send(s);
)}
)
```

Now we can move this to the Pi using SCP. Open a new terminal window and use the following command 
```sh
$ scp *Local/File/sine.sc* ccrma@192.168.105.106:~/supercollider/synthdefs
```

## Start SuperCollider
Switch back to the other terminal window in which you have ssh'd into the Pi.

Run your synthdef script to start SuperCollider and load your synthdef. 

```sh
$ sclang ~/SuperCollider/synthdefs/sine.sc
```

By default, SC runs on port **57110**

## Communicate with SuperCollider

Back on your local machine, open supercollider and run 
```
s = Server("rpi", NetAddr("192.168.105.106",57110));
```

You've now assigned the variable rpi to the SC server running on the Pi.

Test your synthdef by sending a message. 
```
s.sendMsg("/s_new", "sine", x = s.nextNodeID, 1, 1, "freq", 450);
```

Plug in headphones or a speaker into the audio jack on the Pi. The audio that comes out will be relatively low quality. "The PWM audio output is limited to 11 bits of depth at 48kHz by clock speed" raspberrypi.org

To stop the synth, send: 
```
s.sendMsg("/n_free", x);
```

Not working? Exit out of sclang, kill jackd, and restart Jack with ideal settings. Then rerun sclang sine.sc and send the start message again.
```sh
$ sudo killall jackd
$ jackd -P84 -p32 -t2000 -d alsa -dhw:0 -p 2048 -n 3 -r 48000 -P &
```