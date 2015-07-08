# Embedded Music

_This repository documents how setup embedded devices, such as the Raspberry Pi for development with audio software at GTCMT._

## Focus

The focus of this section is to evaluate whether SuperCollider is a feasible development environment on the Raspberry Pi. Currently, I've found that specific versions of packages, such as the Jack Driver and X11, are extremely crucial to development. For this reason the following set of tutorials use the CCRMA Satellite build of the Raspberry Pi. Other hurdles still exist and have yet to be resolved. 

Overall, Supercollider works well for internal synthesis, but realtime audio processing is still limited due to a reliance on the Jack Driver. Other issues with updating packages, using WIFI, Arduino, USB Audio and Quarks exist. This reference is an attempt to document, clarify and hopefully resolve some of these hurdles for future students. This wiki is open and additional findings and documentation would be appreciated.

## Tutorials

* [Setup Your Pi](/tutorials/Setup_Your_Pi.md)
* [Sharing your network with Pi (OSX)](/tutorials/Sharing_your_network_with_Pi_(OSX).md)
* [Running SuperCollider on Pi](/tutorials/Running_SuperCollider_on_Pi.md)
* [Using a USB Audio Interface with Pi](/tutorials/Using_a_USB_Audio_Interface_with_Pi.md)
* [Installing Quarks on Pi](/tutorials/Installing_Quarks_on_Pi.md)
* [Compiling SuperCollider with PortAudio](/tutorials/Compiling_SuperCollider_with_PortAudio.md)
* [Setting up WIFI with GTother](/tutorials/Setting_up_WIFI_with_GTother.md)
* [Arduino & SuperCollider](/tutorials/Arduino_SuperCollider.md)
* [Failed Attempts](/tutorials/Failed_Attempts.md)