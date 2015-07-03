# Embedded Music

_This repsitory documents how setup embedded devices, such as the Raspberry Pi for development with audio software at GTCMT._

## Focus

The focus of this section is to evaluate whether SuperCollider is a feasible development environment on the Raspberry Pi. Currently, I've found that specific versions of packages, such as the Jack Driver and X11, are extremely crucial to development. For this reason the following set of tutorials use the CCRMA Satellite build of the Raspberry Pi. Other hurdles still exist and have yet to be resolved. Overall, Supercollider works well for internal synthesis, but realtime audio processing is still limited due to a reliance on the Jack Driver. Other issues with updating packages, using WIFI, Arduino, USB Audio and Quarks exist. This reference is an attempt to document, clarify and hopefully resolve some of these hurdles for future students. This wiki is open and additional findings and documentation would be appreciated.

## Tutorials

* Sharing your network with Pi (OSX)
* Running SuperCollider on Pi
* Using a USB Audio Interface with Pi
* Installing Quarks on Pi
* Compiling SuperCollider with PortAudio
* Setting up WIFI with GTother
* Arduino & SuperCollider
* Failed Attempts