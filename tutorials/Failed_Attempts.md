# Failed Attempts

While many of these tutorials were successful, I had countless attempts that failed. The purpose of this page is to document things that were difficult or did not work for me. Hopefully with some further investigation and time, I can iron out some of these issues.


## Sharing on GTWifi

This appears to be entirely blocked. As soon as I setup sharing on GTWifi, I receive an error message on my OSX machine: "Your Internet Connection cannot be shared because it is protected..."

## Realtime Audio Processing (Input and Output) with a USB Audio Interface

I eluded to this in the [Using a USB Audio Interface with Pi](Using_a_USB_Audio_Interface_with_Pi.md) tutorial. At the bottom, I mention that Capture and Playback does not work with the Jack driver due to xruns. I discovered that this is a relatively known issue. One theoretical workaround is to directly use the PortAudio driver, however Supercollider needs to be recompiled specifically with this flag. I have created the stub [Compiling SuperCollider with PortAudio](Compiling_SuperCollider_with_PortAudio.md) for future reference.