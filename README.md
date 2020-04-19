# Unified GroundSdk

![Unified GroundSdk](https://user-images.githubusercontent.com/1299716/72654391-7c65a780-395d-11ea-870d-303f2e525234.png)

This fork contains native and Android support for the following Parrot drones:

* Mambo w/Minicam (Wi-Fi only)
* Bebop V1
* Bebop V2
* Disco
* Anafi 4K
* Anafi 4K Thermal

And controllers:

* SkyController V1 (both variants)
* SkyController V2
* SkyController V3

### Support / Questions
This is NOT a Parrot supported project.  Please do not expect or request Parrot, or any of its affiliates, to engage around support questions for code / functionality coming out of this fork.  Feel free to open a Github issue for any items requiring attention within their appropriate (forked) repos on Github.

#### arsdk-ng
This repo houses the core native code shared across the GroundSdk framework.  It has been forked [here](https://github.com/UnifiedGroundSdk/arsdk-ng).  Changes to it to support the unified framework are within the main device connection phase to ensure "legacy" attributes such as the RTP (arstream2) control and data ports are being provided to those devices.

#### arsdk-xml
This repo houses the xml representation of all ARSDK commands.  All Arsdk Feature classes and commands and events are generated from this package.  It has been forked [here](https://github.com/UnifiedGroundSdk/arsdk-xml).  Changes to it to support the unified framework are re-exposing legacy commands such as Flat Trim.

#### groundsdk-android
This repo houses the bulk of all changes (to date) to GroundSdk to expose Android support for the Mambo (Miniature), Bebop, and Disco drones.  It has been forked [here](https://github.com/UnifiedGroundSdk/groundsdk-android).  All device, instrument, peripheral, and customizations are within this repo.

#### groundsdk-product
This repo houses the build configuration details for the entire GroundSdk framework (product).  It has been forked [here](https://github.com/UnifiedGroundSdk/groundsdk-product).  A change to this repo is required for enabling builds of the libMavlink library which is required for the generation of Mavlink (Flightplan) files.

#### librtsp
This repo houses the protocol definitions and instructions for supporting the RTSP protocol.  It has been forked [here](https://github.com/UnifiedGroundSdk/librtsp).  A single change has been made to this library to bypass processing of the RTSP DATE header.   This was necessary because the Mambo drone's RTSP server does not set its DATE header in a standard ISO format.  Since the value of this header is not used downstream, I chose to simply bypass processing it.

#### libMavlink
This repo houses the Mavlink semantics (Mission / MissionItem) for generating a Mavlink file.  It has been forked [here](https://github.com/UnifiedGroundSdk/libMavlink).  A (use specific) change was made to this library to enable the persistence of Param3 values between the native and java layers when copying MissionItems.  

### Helpful Links
#### Arsdk (Legacy) 
All: https://developer.parrot.com/docs/reference/all/index.html <br/>
Bebop: https://developer.parrot.com/docs/reference/bebop/index.html <br/>
SkyController: https://developer.parrot.com/docs/reference/skycontroller/index.html <br/>

SkyController V1 Developer Reference: https://developer.parrot.com/docs/SDK3/SkyControllerDev.pdf <br/>

#### GroundSdk
GroundSdk Reference: https://developer.parrot.com/docs/refdoc-android/index.html <br/>
FlightPlan (MAVLINK) Reference: https://developer.parrot.com/docs/mavlink-flightplan/ <br/>
Install & Build GroundSdk: https://developer.parrot.com/docs/groundsdk-android/buildgroundsdk.html <br/>

#### Sphinx
Sphinx Guidebook:  https://developer.parrot.com/docs/sphinx/ <br/>

### How to Build
Follow Parrot's documentation for installing and building GroundSdk and at the _**repo init**_ step, replace the Parrot groundsdk-manifest repo reference with this one, like so:

![Replace the Parrot Developers groundsdk-manifest repo reference](https://user-images.githubusercontent.com/1299716/72654400-81c2f200-395d-11ea-870d-476d0345fb79.png)

becomes:
```
repo init -u https://github.com/UnifiedGroundSdk/groundsdk-manifest
```

### What's Broke?
First off it is important to note that not all functionality has been tested on all devices at this time.  It is quite a bit for one person to juggle during the Winter months but I would estimate at this point the project overall is about 90% stable.  I have spent a considerable amount of time with my Anafi and Bebop2 drones powered up in my livingroom plus even more time with a VM based instance of Sphinx running.

You don't know what you don't know and it applies here.  What I do know is:

* Gamepad mappings for the SC1 are not yet implemented
* Gamepad mappings for the SC2 are incomplete / mapped incorrectly
* Mini mappings for the Flypad are not yet implemented (I may never implement them)
* Mambo signal RSSI is reported based on Android signal strength.  The Mambo will never provide this data as this is a drone firmware bug that I have worked around.
* Mambo will never transition from the hovering to flying state.  This is a drone firmware bug that never got fixed.
* Bebop / Disco Timelapse is broken.  I have some ideas for working around this but, similar to Mambo RSSI, this is broken within the drone firmware and will never be fixed by Parrot.
* There are likely lots of functional holes for the Bebop V1 that will never get filled due to it missing the Animation and Follow Me feature sets.  Perhaps I'll emulate this within GroundSdk at some point.  See how I have the Mambo reporting GPS coordinates even though it doesn't have a GPS to get an idea of what is possible.


### Licensing Note
Apache Commons Net (https://commons.apache.org/proper/commons-net/), specifically its FTP client, has been localized within this project for ease of integration.  Please see the Apache License here for further details:  http://www.apache.org/licenses/

As per Parrot SA, in regards to all other remaining code (where applicible - other licenses do apply):

    Copyright (C) 2019 Parrot Drones SAS

    Redistribution and use in source and binary forms, with or without
    modification, are permitted provided that the following conditions
    are met:
    - Redistributions of source code must retain the above copyright
      notice, this list of conditions and the following disclaimer.
    - Redistributions in binary form must reproduce the above copyright
      notice, this list of conditions and the following disclaimer in
      the documentation and/or other materials provided with the
      distribution.
    - Neither the name of the Parrot Company nor the names
      of its contributors may be used to endorse or promote products
      derived from this software without specific prior written
      permission.

    THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
    "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
    LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
    FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
    PARROT COMPANY BE LIABLE FOR ANY DIRECT, INDIRECT,
    INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
    BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
    OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
    AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
    OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT
    OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
    SUCH DAMAGE.


