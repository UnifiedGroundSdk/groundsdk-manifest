# Ground SDK

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
This is NOT a Parrot supported project.  Please do not expect or request Parrot, or any of its affiliates, to engage around support questions for code / functionality coming out of this fork.  Feel free to open a Github issue for any items requiring attention within their appropriate repos.  

#### arsdk-ng
This repo houses the core native code shared across the GroundSdk framework.  It has been forked [here](https://github.com/synman/arsdk-ng).  Changes to it to support the unified framework are within the main device connection phase to ensure "legacy" attributes such as the RTP (arstream2) control and data ports are being provided to those devices.

#### groundsdk-android
This repo houses the bulk of all changes (to date) to GroundSdk to expose Android support for the Mambo (Miniature), Bebop, and Disco drones.  It has been forked [here](https://github.com/synman/groundsdk-android).  All device, instrument, peripheral, and customizations are within this repo.

#### groundsdk-product
This repo houses the build configuration details for the entire GroundSdk framework (product).  It has been forked [here](https://github.com/synman/groundsdk-product).  A change to this repo is required for enabling builds of the libMavlink library which is required for the generation of Mavlink (Flightplan) files.

#### librtsp
This repo houses the protocol definitions and instructions for supporting the RTSP protocol.  It has been forked [here](https://github.com/synman/librtsp).  A single change has been made to this library to bypass processing of the RTSP DATE header.   This was necessary because the Mambo drone's RTSP server does not set its DATE header in a standard ISO format.  Since the value of this header is not used downstream, I chose to simply bypass processing it.

#### libMavlink
This repo houses the Mavlink semantics (Mission / MissionItem) for generating a Mavlink file.  It has been forked [here](https://github.com/synman/libMavlink).  A (use specific) change was made to this library to enable the persistence of Param3 values between the native and java layers when copying MissionItems.  

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


