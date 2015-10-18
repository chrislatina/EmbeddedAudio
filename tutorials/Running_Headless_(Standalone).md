# Running Headless (Standalone)

This tutorial will cover how to startup running a script (in this case a csound instrument) without the need for ssh or an external computer,  a.k.a. running "headless". This tutorial was taken from csounds.com

## Configuring Auto-Login

To set it up your device so that it automatically logs in at start-up, edit the `/etc/inittab file` with administrative privileges.

Run nano to edit the file `/etc/inittab` with administrative privilages:

```sh
sudo vim /etc/inittab
```
Scroll down using the arrow keys to this line:

```sh
1:2345:respawn:/sbin/getty --noclear 38400 tty1
```
Comment it out with the # character so that it looks like this:

```sh
#1:2345:respawn:/sbin/getty 115200 tty1
```

Write this line underneath it, substituting "USERNAME" with the name of the user to be logged in.

```sh
1:2345:respawn:/bin/login -f USERNAME tty1 /dev/tty1 2>&1
```

for our pi, it should use ccrma as the username

```sh
1:2345:respawn:/bin/login -f ccrma tty1 /dev/tty1 2>&1
```


Enter :X to exit vim and save. When the device is rebooted it will login automatically, and this can be verified by connecting a monitor to the Raspberry Pi, or to the BeagleBone with a video output cape. If a mistake is made and the device hangs on boot, entering ctrl-alt-f2 will allow you to login using the next virtual terminal window, where /etc/inittab can be repaired. Note that if the screen application is being used to monitor the device, it will not recognize the automatic login and login will still need to be performed manually.

## Execute Csound at Boot

When using your device as a musical instrument, Csound will need to start automatically. Once automatic log-in is setup for your device, commands can be added to the file in ~/.bash_profile, which will be executed after the login process. To do this, run the command:

```sh
nano ~/.bash_profile
```

Then add the following line:
```sh
csound foo.csd
```

"foo.csd" should be the name of the .csd file to be executed at boot. If the directory is not explicitly navigated to with the cd command, Csound will automatically look for the .csd in the home (~) directory. If all the necessary command-line flags are added in the CsOptions part of the .csd, then there is no need to set any flags in ~/.bash_profile. The next time the device reboots, the .csd will automatically execute after automatically logging in.

To run Csound in the background, thus enabling other programs to be executed concurrently, add an ampersand to the end of the command in ~/.bash_profile:
```sh
csound foo.csd &
```
To stop Csound from running, execute the following command:
```sh
sudo killall csound
```

Csound can also be executed from the file /etc/rc.local, but ~/.bash_profile is more convenient because it does not need root privileges.

## References
* [csounds.com](http://www.csounds.com/journal/issue18/beagle_pi.html)